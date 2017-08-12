---
layout: post
title:  shell脚本变量和字符串截取
date:   2017-07-20
tag: linux 学习
---

注：内容转载自网络，暂时没有找到出处，如果有人知道作者是谁，请与我联系，我好标明版权信息

### 变量说明

$ Shell本身的PID（ProcessID）

$! Shell最后运行的后台Process的PID

$? 最后运行的命令的结束代码（返回值）

$- 使用Set命令设定的Flag一览

$* 所有参数列表。如”$*”用「”」括起来的情况、以”$1 $2 … $n”的形式输出所有参数。

$@ 所有参数列表。如”$@”用「”」括起来的情况、以”$1″ “$2″ … “$n” 的形式输出所有参数。

$# 添加到Shell的参数个数

$0 Shell本身的文件名

$1～$n 添加到Shell的各参数值。$1是第1参数、$2是第2参数……
 
### 字符串截取

shell中截取字符串的方法有很多中，可以分为两大类。第一种获取特定的字符或字符串的左边或者右边的字字符串，java中实现需要先用indexOf来确定特定字符串的位置，然后再用substring来获取结果；第二种类似java中的substring
shell中截取字符串的方法有很多中，

${expression}一共有9种使用方法。

${parameter:-word}

${parameter:=word}

${parameter:?word}

${parameter:+word} 

上面4种可以用来进行缺省值的替换。

${#parameter}

上面这种可以获得字符串的长度。 

${parameter%word} 最小限度从后面截取word

${parameter%%word} 最大限度从后面截取word

${parameter#word} 最小限度从前面截取word

${parameter##word} 最大限度从前面截取word

上面4个就是用来截取字符串的方法了。

有了着四种用法就不必使用cut命令来截取字符串了

第一种又可以分为四种情况，下面一一介绍。

1、使用 # 号操作符。用途是从左边开始删除第一次出现子字符串即其左边字符，保留右边字符。用法为#*substr,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${str#*//}

得到的结果为www.你的域名.com/cut-string.html，即删除从左边开始到第一个"//"及其左边所有字符2、使用 ## 号操作符。用途是从左边开始删除最后一次出现子字符串即其左边字符，保留右边字符。用法为##*substr,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${str##*/}

得到的结果为cut-string.html，即删除最后出现的"/"及其左边所有字符3、使用 % 号操作符。用途是从右边开始删除第一次出现子字符串即其右边字符，保留左边字符。用法为%substr*,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${str%/*}

得到的结果为http://www.你的域名.com，即删除从右边开始到第一个"/"及其右边所有字符4、使用 %% 号操作符。用途是从右边开始删除最后一次出现子字符串即其右边字符，保留左边字符。用法为%%substr*,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${str%%/*}

得到的结果为http://www.你的域名.com，即删除从右边开始到最后一个"/"及其右边所有字符第二种也分为四种，分别介绍如下：
1、从左边第几个字符开始以及字符的个数，用法为:start:len,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${var:0:5}

其中的 0 表示左边第一个字符开始，5 表示字符的总个数。

结果是：http:2、从左边第几个字符开始一直到结束，用法为:start,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${var:7}

其中的 7 表示左边第8个字符开始

结果是：www.你的域名.com/cut-string.html3、从右边第几个字符开始以及字符的个数，用法:0-start:len,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${str:0-15:10}

其中的 0-6 表示右边算起第6个字符开始，10 表示字符的个数。

结果是：cut-string3、从右边第几个字符开始一直到结束，用法:0-start,例如：

str='http://www.你的域名.com/cut-string.html'

echo ${str:0-4}

其中的 0-6 表示右边算起第6个字符开始，10 表示字符的个数。

结果是：html注：（左边的第一个字符是用 0 表示，右边的第一个字符用 0-1 表示）

网上其它参考内容

一、Linux shell 截取字符变量的前8位，有方法如下：

1.expr substr “$a” 1 8
2.echo $a|awk ‘{print substr(,1,8)}’
3.echo $a|cut -c1-8
4.echo $
5.expr $a : ‘(.\).*’
6.echo $a|dd bs=1 count=8 2>/dev/null
二、按指定的字符串截取

1、第一种方法:

${varible##*string} 从左向右截取最后一个string后的字符串

${varible#*string}从左向右截取第一个string后的字符串

${varible%%string*}从右向左截取最后一个string后的字符串

${varible%string*}从右向左截取第一个string后的字符串

“*”只是一个通配符可以不要

例子：

$ MYVAR=foodforthought.jpg

$ echo ${MYVAR##*fo}

rthought.jpg

$ echo ${MYVAR#*fo}

odforthought.jpg

2、第二种方法：${varible:n1:n2}:截取变量varible从n1到n2之间的字符串。

可以根据特定字符偏移和长度，使用另一种形式的变量扩展，来选择特定子字符串。试着在 bash 中输入以下行：

$ EXCLAIM=cowabunga

$ echo ${EXCLAIM:0:3}

cow

$ echo ${EXCLAIM:3:7}

abunga

这种形式的字符串截断非常简便，只需用冒号分开来指定起始字符和子字符串长度。

三、按照指定要求分割：

比如获取后缀名

ls -al | cut -d “.” -f2
