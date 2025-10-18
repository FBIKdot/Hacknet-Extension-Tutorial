# HackerScripts (黑客脚本)
HackerScript 用于描述黑客行为, 比如入侵, 文件操作等等. 它可以通过行为标签`<LaunchHackScript>`执行.  

HackerScript 的执行具有实时性. HackerScript内的任何间隔与行为标签的`delay`原理不同. 因此退出重进Hacknet将会使正在执行中的HackerScript停止. HackerScript被执行后的效果与玩家有部分相似之处, 比如会留下日志.

以下为HackerScript的大致结构: 
~~~
# 指定目标
config playerComp advExamplePC 0.2 $#%#$

# 行为
connect $#%#$
disconnect $#%#$

# 这里的"注释"是不规范写法, 因为没有对应命令不会被执行. 官方没有为HackerScript提供注释
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

| 行为类型 | 功能 | 参数个数 | 参数用途 |
| --- | --- | --- | --- |
| `connect` | 源电脑向目标电脑建立连接 | 无 | |
| `delay` | 用来延迟一段时间 | 一个 | 延迟时间，单位为秒 |
| `openPort` | 打开目标电脑的端口 | 一个 | 要开启的端口 |
| `clearTerminal` | 清屏目标电脑终端 | 无 | |
| `hideNetMap` | 隐藏目标电脑的netmap网络地图 | 无 | |
| `hideRam` | 隐藏目标电脑的RAM区域 | 无 | |
| `hideDisplay` | 隐藏目标电脑的显示Display区域 | 无 | |
| `hideTerminal` | 隐藏目标电脑的终端 | 无 | |
| `showNetMap` | 显示目标电脑的netmap网络地图 | 无 | |
| `showRam` | 显示目标电脑的RAM区域 | 无 | |
| `showDisplay` | 显示目标电脑的显示Display区域 | 无 | |
| `showTerminal` | 显示目标电脑的终端 | 无 | |
| `trackseq` | 改变玩家被forkbomb成功的结果 | 无 | 如果有CSEC flag并且没有防御成功forkbomb，则进入紧急恢复模式(不会蓝屏) |
| `instanttrace` | 立即使目标电脑进入紧急恢复模式 | 无 | |
| `forkbomb` | 为目标电脑执行forkbomb | 无 | |
| `flash` | 让目标电脑的UI闪烁一下 | 无 | |
| `delete` | 删除目标电脑上的文件 | 两个 | 目标文件所在路径和目标文件名 |
| `setAdminPass` | 设置目标电脑上的管理员密码 | 一个 | 要设定的新管理员密码 |
| `makeFile` | 在目标电脑上新建一个文件 | 三个 | 1.要创建的文件所在目录，2.要创建的文件名，3.文件内容 |
| `openCDTray` | 打开目标电脑的光驱 | 无 | |
| `closeCDTray` | 关闭目标电脑上的光驱 | 无 | |
| `disconnect` | 断开目标电脑 | 无 | |
| `write` | 在目标电脑终端中输出字符，但不换行 | 一个 | 要输出的字符串 |
| `writel` | 在目标电脑终端中输出字符并换行 | 一个 | 要输出的字符串 |
| `writel_silent` | 在目标电脑终端中输出字符并换行，但不会使目标UI变红闪烁一下 | 一个 | 要输出的字符串 |
