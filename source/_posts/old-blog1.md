title: RSA加密算法在iOS9下的问题解决方案 #可以改成中文的，如“新文章”
date: 2015-10-31 19:04 #发表日期，一般不改动
tags: [iOS]
categories: 主攻击技能 #文章文类
---

本人于2015年5月写的可运行的RSA加密解密算法，升级到iOS9之后，到`SecItemAdd`就crash掉了。
打了断点发现SecKeyRef竟然为空，几个月前可不是这样的，只能是iOS9更新了什么。看了一下官方文档：[About the security content of iOS 9](https://support.apple.com/en-us/HT205212)
>CFNetwork SSL
Available for: iPhone 4s and later, iPod touch (5th generation) and later, iPad 2 and later
Impact: An attacker may be able to decrypt data protected by SSL
Description: There are known attacks on the confidentiality of RC4. An attacker could force the use of RC4, even if the server preferred better ciphers, by blocking TLS 1.0 and higher connections until CFNetwork tried SSL 3.0, which only allows RC4. This issue was addressed by removing the fallback to SSL 3.0.

大概就是说，旧的网络方式被破了，所以换成了SSL 3.0的。SSL 3.0用的是RSA加密，所以，我觉得是苹果认为觉得自己新的连接方式比较安全，不需要双层加密吧。（当然也有可能是苹果的bug，[Import of RSA key crashes on iOS9](https://github.com/AArnott/PCLCrypto/issues/29))

---

在[@xillkey](http://weibo.com/u/1794589962)的启发下想到一个曲折救国的解决方案：
###就是偷偷新建一个web view把加密的算法用javascript执行，曲线救国

首先，在项目里新建一个rsa.html，然后写上以下代码：
```html
<html>
    <head>
    <script type="text/javascript" src="jsbn.js" ></script>
    <script type="text/javascript"src="prng4.js" ></script>
    <script type="text/javascript" src="rng.js" ></script>
    <script type="text/javascript" src="rsa.js" ></script>
    <script type="text/javascript">
        var cipher = new RSAKey();
        </script>
    </head>
</html>
```

之后在对应的.m文件下写上：
```objective-c
@property (nonatomic, strong) UIWebView *web;

- (void) viewDidLoad{
	_web = [[UIWebView alloc] init];
    NSString *path = [[NSBundle mainBundle] bundlePath];
    NSURL *baseURL = [NSURL fileURLWithPath:path];
    NSString * htmlPath = [[NSBundle mainBundle] pathForResource:@"rsa"
                                                          ofType:@"html"];
    NSString * htmlCont = [NSString stringWithContentsOfFile:htmlPath
                                                    encoding:NSUTF8StringEncoding
                                                       error:nil];
    
    [_web loadHTMLString:htmlCont baseURL:baseURL];
}

- (void)function:(NSString *)modulus exponent:(NSString *)exponent {       
        [_web stringByEvaluatingJavaScriptFromString:[[NSString alloc] initWithFormat:@"cipher.setPublic('%@','%@');",modulus,exponent]];
        NSString *hexStr = [_web stringByEvaluatingJavaScriptFromString:[[NSString alloc] initWithFormat:@"cipher.encrypt('%@')",_passwordTextField.text]];

}
```

**hexStr就是你想要的rsa加密过的密码（或者别的什么东西）**啦～本来理论上可以用c语言根据rsa算法公式写出c语言版本的加密解密文件，后来有小伙伴提醒道苹果时不允许自己写rsa只能用他的2048位，所以突然不爽苹果决定用另一个方案解决，跳过Objective-c。

本解决方案还需要在项目中四个js文件，下载地址：[rsa的js文件](http://download.csdn.net/detail/u010558548/9229941)

感谢js的作者带给我新思路，还有，如果有什么大神路过觉得我这个办法可以有更好的解决方案，非常希望教授经验。

---

在以下网址中可以得到其他的，用正常的处理方案（我觉得用js有点投机取巧了）：
https://forums.developer.apple.com/thread/15129
https://forums.developer.apple.com/message/38361#38361
StCredZero/SCZ-BasicEncodingRules-iOS#6 (comment)
具体的解决方案在
https://github.com/AArnott/PCLCrypto/issues/29
差不多结束的对话里。

还有：http://blog.iamzsx.me/show.html?id=155002
这博客的处理方案经实验验证，也是可以在iOS9上跑通的。

---

最后，这篇文章的原文在这里：[my csdn blog](http://blog.csdn.net/suusatoshigi/article/details/49535391)
