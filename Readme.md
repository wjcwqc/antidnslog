# 如何反制ceye.io 等固定二级域名的DNSlog平台

下面所述一些脚本就不放出来了，基本可以python自己实现。

## 方案一
社工获得二级头（二级域名的头部，下简称二级头）对应的账号信息。  
也就是通过"hehehe.ceye.io"中的二级头"hehehe"社工方式找到对应用户。这也是固定二级头的弊端。
## 方案二 
**以下操作请使用手机热点**
1. 手机装个linux，docker或者chroot均可，简单点，开启热点关闭wifi。或者简单点电脑连手机热点。
1. 全局替换dns.txt中的二级头。或者自己修改dig列表。
1. 使用命令```dig -f dns.txt```  
1. 具体效果自己可以测试一下，根据运营商不同dns类型数量也不同。江苏电信一下可以跑几十条dns记录且没有自己的热点ip。
1. 测试完效果最好的dns反射类型之后可以生成混乱前缀，亲测punycode或者中文编码反射效率较低。最后使用持续化、多线程脚本跑dnslog进行轰炸。

注：该方法对网上常见自建dnslog平台同样有效。

## 高级玩法
1. 可以把dnslog请求让蜜罐返回去，具体原因dddd。稍微nb点蜜罐说不定就能实现[方案一](#方案一)甚至直接拿下账号。
1. 用拼音发点恶心心的dns请求刷屏比较基本了，可以选择用http请求混合dns请求定向poc轰炸那些直接武器化的攻击。让武器一直报洞影响正常使用。定向poc可以根据攻击者攻击推断出来，如前缀hex递增，或者请求javaversion的等。
1. 还有一些结合其他攻击行为联合反制，如直接让vps无法请求dnslog平台的api等。

都说是以攻促防，希望各大厂也能给点力，出点有用的工具反制***攻击队***和攻击。