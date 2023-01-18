# HackerScripts
HackerScript用来模拟别的黑客的反击，如naix  
这是一个HackerScript的例子:  
```
config playerComp advExamplePC 0.2 $#%#$
connect $#%#$
delay 3.3 $#%#$
openPort 22 $#%#$
delay 1.3 $#%#$
openPort 21 $#%#$
delay 1.3 $#%#$
openPort 80 $#%#$
disconnect $#%#$
```   
在这个HackerScript中，第一行使用了```config playerComp advExamplePC 0.2 $#%#$```，它用来初始化这个HackerScript，这一行，指定了目标，原电脑，延迟，它的用法如下:  
`config \[目标电脑ID\] \[源电脑ID\] \[每一行执行的延迟\] $#%#$`  
ps:`$#%#$` 是必须的，用来在后面的代码中指定攻击属性，它必须为`$#%#$`，否则无效  
后面就可以使用代码来实现功能，但必须在每一行后加上`$#%#$`，参数之间用空格分隔  
目前可用的功能有:
- connect 不需要任何额外参数，表示从源电脑向目标电脑建立连接
- delay 用来延迟一段时间，有一个参数是延迟时间，单位为秒
- openPort 打开目标电脑的端口，有一个参数，指的是要开启的端口
- writel 在目标电脑终端中输出字符，有一个参数，指的是要输出的字符串
- clearTerminal 清屏目标电脑终端，无额外参数
- hideNetMap 隐藏目标电脑的netmap网络地图，无额外参数
- hideRam 隐藏目标电脑的RAM区域，无额外参数
- hideDisplay 隐藏目标电脑的显示Display区域，无额外参数
- hideTerminal 隐藏目标电脑的终端，无额外参数
- showNetMap 显示目标电脑的netmap网络地图，无额外参数
- showRam 显示目标电脑的RAM区域，无额外参数
- showDisplay 显示目标电脑的显示Display区域，无额外参数
- showTerminal 显示目标电脑的终端，无额外参数
- trackseq 为目标电脑加flag，如果有CSEC flag并且没有防御成功forkbomb，则进入紧急恢复模式(不会启动forkbomb)，无额外参数
- instanttrace 立即使目标电脑进入紧急恢复模式
- forkbomb 为目标电脑执行forkbomb
- flash 让目标电脑的UI闪烁一下，无额外参数
- delete 删除目标电脑上的文件，有两个参数，目标文件所在路径和目标文件名
- setAdminPass 设置目标电脑上的管理员密码，有一个参数，是要设定的新管理员密码
- makeFile 在目标电脑上新建一个文件，有三个参数:1.要创建的文件所在目录，要创建的文件名，文件内容
- openCDTray 打开目标电脑的光驱，无额外参数
- closeCDTray 关闭目标电脑上的光驱，无额外参数
- disconnect 断开目标电脑，无额外参数