# HackerScripts (黑客脚本)
HackerScript 用于描述黑客行为, 比如入侵, 文件操作等等. 它可以通过行为标签`<LaunchHackScript>`执行.  

HackerScript 的执行具有实时性. HackerScript内的任何间隔与行为标签的`delay`原理不同. 因此退出重进Hacknet将会使正在执行中的HackerScript停止. HackerScript被执行后的效果与玩家有部分相似之处, 比如会留下日志.

这是一个HackerScript示范: 
~~~
config playerComp advExamplePC 0.2 $#%#$
connect $#%#$
delay 3.3 $#%#$
openPort 22 $#%#$
delay 1.3 $#%#$
openPort 21 $#%#$
delay 1.3 $#%#$
openPort 80 $#%#$
disconnect $#%#$
~~~

HackerScript的内容可以大致分为:

- 指定目标
- 行为

# 指定目标
config用于指定了目标，源电脑，每一行执行之间的间隔，格式如下如下:  
~~~
config [目标电脑ID] [源电脑ID] [每一行执行的延迟] $#%#$
~~~
如果你想要通过标签来选择目标于源电脑的话, 可以原封不动这么写ID, 然后在标签中声明相应属性:
~~~
config [TARGET_COMP] [SOURCE_COMP] 0 $#%#$
~~~

一个HackerScript可以指定多个目标, 但是不是同时攻击.
~~~
config TARGET_COMP1 SOURCE_COMP1 0 $#%#$
...
config TARGET_COMP2 SOURCE_COMP1 0 $#%#$
...
~~~
# 行为
可以使用行为语句来描述行为, 行为语句相应的行为将会被执行. 

行为语句大致如下:
~~~
[行为类型] [...参数] $#%#$
~~~
行为类型与`$#%#$`为必须内容, 部分行为不需要参数.

行为类型如下:
- `connect` 源电脑向目标电脑建立连接, 无参数
- `delay` 用来延迟一段时间，有一个参数是延迟时间，单位为秒
- `openPort` 打开目标电脑的端口，有一个参数，指的是要开启的端口
- `clearTerminal` 清屏目标电脑终端, 无参数
-` hideNetMap` 隐藏目标电脑的netmap网络地图, 无参数
- `hideRam` 隐藏目标电脑的RAM区域, 无参数
- `hideDisplay` 隐藏目标电脑的显示Display区域, 无参数
- `hideTerminal` 隐藏目标电脑的终端, 无参数
- `showNetMap` 显示目标电脑的netmap网络地图, 无参数
- `showRam` 显示目标电脑的RAM区域, 无参数
- `showDisplay` 显示目标电脑的显示Display区域, 无参数
- `showTerminal` 显示目标电脑的终端, 无参数
- `trackseq` 为目标电脑加flag，如果有CSEC flag并且没有防御成功forkbomb，则进入紧急恢复模式(不会启动forkbomb), 无参数
- `instanttrace` 立即使目标电脑进入紧急恢复模式
- `forkbomb `为目标电脑执行forkbomb
- `flash` 让目标电脑的UI闪烁一下, 无参数
- `delete` 删除目标电脑上的文件，有两个参数，目标文件所在路径和目标文件名
- `setAdminPass` 设置目标电脑上的管理员密码，有一个参数，是要设定的新管理员密码
- `makeFile` 在目标电脑上新建一个文件，有三个参数: 1.要创建的文件所在目录，要创建的文件名，文件内容
- `openCDTray` 打开目标电脑的光驱, 无参数
- `closeCDTray` 关闭目标电脑上的光驱, 无参数
- `disconnect` 断开目标电脑, 无参数
- `write` 在目标电脑终端中输出字符，但不换行，有一个参数，指的是要输出的字符串
- `writel` 在目标电脑终端中输出字符并换行，有一个参数，指的是要输出的字符串
- `writel_silent` 在目标电脑终端中输出字符并换行，但不会使目标UI变红闪烁一下，有一个参数，指的是要输出的字符串