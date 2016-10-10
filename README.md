# -

转自http://blog.csdn.net/chaoyuan899/article/details/38583759
 iOS常用正则表达式
正则表达式用于字符串处理、表单验证等场合，实用高效。现将一些常用的表达式收集于此，以备不时之需。

匹配中文字符的正则表达式： [\u4e00-\u9fa5]
评注：匹配中文还真是个头疼的事，有了这个表达式就好办了

匹配双字节字符(包括汉字在内)：[^\x00-\xff]
评注：可以用来计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）

匹配空白行的正则表达式：\n\s*\r
评注：可以用来删除空白行

匹配HTML标记的正则表达式：<(\S*?)[^>]*>.*?</\1>|<.*? />
评注：网上流传的版本太糟糕，上面这个也仅仅能匹配部分，对于复杂的嵌套标记依旧没有能力为力

匹配首尾空白字符的正则表达式：^\s*|\s*$
评注：可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式

匹配Email地址的正则表达式：\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*
评注：表单验证时很实用

匹配网址URL的正则表达式：[a-zA-z]+://[^\s]*
评注：网上流传的版本功能很有限，上面这个基本可以满足需求

匹配帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$
评注：表单验证时很实用

匹配国内电话号码：\d{3}-\d{8}|\d{4}-\d{7}
评注：匹配形式如 0511-4405222 或 021-87888822

匹配腾讯QQ号：[1-9][0-9]{4,}
评注：腾讯QQ号从10000开始

匹配中国邮政编码：[1-9]\d{5}(?!\d)
评注：中国邮政编码为6位数字

匹配身份证：\d{15}|\d{18}
评注：中国的身份证为15位或18位

匹配ip地址：\d+\.\d+\.\d+\.\d+
评注：提取ip地址时有用

匹配特定数字：
^[1-9]\d*$　 　 //匹配正整数
^-[1-9]\d*$ 　 //匹配负整数
^-?[1-9]\d*$　　 //匹配整数
^[1-9]\d*|0$　 //匹配非负整数（正整数 + 0）
^-[1-9]\d*|0$　　 //匹配非正整数（负整数 + 0）
^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$　　 //匹配正浮点数
^-([1-9]\d*\.\d*|0\.\d*[1-9]\d*)$　 //匹配负浮点数
^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$　 //匹配浮点数
^[1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0$　　 //匹配非负浮点数（正浮点数 + 0）
^(-([1-9]\d*\.\d*|0\.\d*[1-9]\d*))|0?\.0+|0$　　//匹配非正浮点数（负浮点数 + 0）
评注：处理大量数据时有用，具体应用时注意修正

匹配特定字符串：
^[A-Za-z]+$　　//匹配由26个英文字母组成的字符串
^[A-Z]+$　　//匹配由26个英文字母的大写组成的字符串
^[a-z]+$　　//匹配由26个英文字母的小写组成的字符串
^[A-Za-z0-9]+$　　//匹配由数字和26个英文字母组成的字符串
^\w+$　　//匹配由数字、26个英文字母或者下划线组成的字符串 

匹配中文:[\u4e00-\u9fa5] 

英文字母:[a-zA-Z] 

数字:[0-9] 

匹配中文，英文字母和数字及_: 
^[\u4e00-\u9fa5_a-zA-Z0-9]+$

同时判断输入长度：
[\u4e00-\u9fa5_a-zA-Z0-9_]{4,10}

^[\w\u4E00-\u9FA5\uF900-\uFA2D]*$ 1、一个正则表达式，只含有汉字、数字、字母、下划线不能以下划线开头和结尾：
^(?!_)(?!.*?_$)[a-zA-Z0-9_\u4e00-\u9fa5]+$  其中：
^  与字符串开始的地方匹配
(?!_)　　不能以_开头
(?!.*?_$)　　不能以_结尾
[a-zA-Z0-9_\u4e00-\u9fa5]+　　至少一个汉字、数字、字母、下划线
$　　与字符串结束的地方匹配

放在程序里前面加@，否则需要\\进行转义 @"^(?!_)(?!.*?_$)[a-zA-Z0-9_\u4e00-\u9fa5]+$"
（或者：@"^(?!_)\w*(?<!_)$"    或者  @" ^[\u4E00-\u9FA50-9a-zA-Z_]+$ "  )

2、只含有汉字、数字、字母、下划线，下划线位置不限：
^[a-zA-Z0-9_\u4e00-\u9fa5]+$

3、由数字、26个英文字母或者下划线组成的字符串
^\w+$

4、2~4个汉字
@"^[\u4E00-\u9FA5]{2,4}$"; 

5、
^[\w-]+(\.[\w-]+)*@[\w-]+(\.[\w-]+)+$

用：(Abc)+    来分析：  XYZAbcAbcAbcXYZAbcAb

XYZAbcAbcAbcXYZAbcAb6、
[^\u4E00-\u9FA50-9a-zA-Z_]
34555#5' -->34555#5'

[\u4E00-\u9FA50-9a-zA-Z_]    eiieng_89_   --->   eiieng_89_
_';'eiieng_88&*9_    -->  _';'eiieng_88&*9_
_';'eiieng_88_&*9_  -->  _';'eiieng_88_&*9_

最长不得超过7个汉字，或14个字节(数字，字母和下划线)正则表达式
^[\u4e00-\u9fa5]{1,7}$|^[\dA-Za-z_]{1,14}$
///----------2014.10.07 再次编辑----------------
匹配月份的正则表达式
^[1-9]$|^1[0-2]$

注：个位数月份匹配方式 前面不能加 0。

^0?[1-9]$|^1[0-2]$

注：个位数月份前可以加0或者不加。

匹配年份19**或者20**

^(19|20)[0-9]{2}$


用法：
[objc] view plain copy print?在CODE上查看代码片派生到我的代码片
+ (BOOL)isEmailAddress:(NSString*)candidate  
{  
    NSString* emailRegex = @"[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}";  
    NSPredicate* emailTest = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegex];  
    return [emailTest evaluateWithObject:candidate];  
}  

[objc] view plain copy print?在CODE上查看代码片派生到我的代码片
-(NSNumber *)asNumber;{  
    NSString *regEx = @"^-?\\d+.?\\d?";  
    NSPredicate * pred      = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", regEx];  
    BOOL isMatch            = [pred evaluateWithObject:self];  
    if (isMatch) {  
        return [NSNumber numberWithDouble:[self doubleValue]];  
    }  
    return nil;  
}  

[objc] view plain copy print?在CODE上查看代码片派生到我的代码片
//摘自NSString+BeeExtension.mm  
- (BOOL)isUserName  
{  
    NSString *      regex = @"(^[A-Za-z0-9]{3,20}$)";  
    NSPredicate *   pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", regex];  
      
    return [pred evaluateWithObject:self];  
}  
  
- (BOOL)isPassword  
{  
    NSString *      regex = @"(^[A-Za-z0-9]{6,20}$)";  
    NSPredicate *   pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", regex];  
      
    return [pred evaluateWithObject:self];    
}  
  
- (BOOL)isEmail  
{  
    NSString *      regex = @"[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,4}";  
    NSPredicate *   pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", regex];  
      
    return [pred evaluateWithObject:self];  
}  
  
- (BOOL)isUrl  
{  
    NSString *      regex = @"http(s)?:\\/\\/([\\w-]+\\.)+[\\w-]+(\\/[\\w- .\\/?%&=]*)?";  
    NSPredicate *   pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", regex];  
      
    return [pred evaluateWithObject:self];  
}  
  
- (BOOL)isTelephone  
{  
    NSString * MOBILE = @"^1(3[0-9]|5[0-35-9]|8[025-9])\\d{8}$";  
    NSString * CM = @"^1(34[0-8]|(3[5-9]|5[017-9]|8[278])\\d)\\d{7}$";  
    NSString * CU = @"^1(3[0-2]|5[256]|8[56])\\d{8}$";  
    NSString * CT = @"^1((33|53|8[09])[0-9]|349)\\d{7}$";  
    NSString * PHS = @"^0(10|2[0-5789]|\\d{3})\\d{7,8}$";  
    NSPredicate *regextestmobile = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", MOBILE];  
    NSPredicate *regextestcm = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", CM];  
    NSPredicate *regextestcu = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", CU];  
    NSPredicate *regextestct = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", CT];  
    NSPredicate *regextestphs = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", PHS];  
  
    return  [regextestmobile evaluateWithObject:self]   ||  
            [regextestphs evaluateWithObject:self]      ||  
            [regextestct evaluateWithObject:self]       ||  
            [regextestcu evaluateWithObject:self]       ||  
            [regextestcm evaluateWithObject:self];  
}  
