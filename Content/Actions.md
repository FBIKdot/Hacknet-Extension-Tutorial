# Actions  
Actions可以实现例如DHS中的对话，DLC中Coel的破坏白名单等，它实现游戏的各种特效，是一个优秀的扩展不可或缺的一部分  
Actions中可以有多个Action，使用相对路径调用  
一个Action的结构大概如下:  
```xml
<ConditionalActions>
    <!--这里是Action的其他代码-->
</ConditionalActions>
```
我们可以看到，Action由```<ConditionalActions>```开始，由```</ConditionalActions>```结束，这是Action的标准格式  
每个Action都有触发条件，也就是达成什么条件时触发  
触发条件共有以下几种，但先决条件都是这个Action被加载:
- Instantly 立即触发 
- OnConnect 连接某个节点后触发，有一个必须属性target，指的是触发需要连接节点的ID
- HasFlags 拥有某项flag(s)后触发，有一个必须属性requiredFlags,指的是触发需要的flag，多个flag用英文逗号分割
- DoesNotHaveFlags 没有某项flag(s)后触发，所需设定属性与HasFlags相同
- OnDisconnect 断开某个节点后触发，所需设定属性与OnConnect相同
- OnAdminGained 获取某个节点的管理员权限后触发，有一个必须属性target，指的是触发需要获取管理员权限的节点ID

这些触发条件都有一些通用的可选属性:  
- needsMissionComplete 当完成当前任务时触发
- requiredFlags 拥有特定flag触发

下面开始正式进行Action实现功能的讲解  
首先，一些Action可以被延迟，如果需要延迟，则应指定两个属性：
- DelayHost 因Hacknet的特性，Action延迟需要一个节点帮助，这个节点就是DelayHost,需要有FastActionHost守护线程，该属性为节点ID
- Delay 延迟时间

## AddIRCMessage
作用:在指定IRC频道发送消息  
属性:
- Author 信息的发送人
- TargetComp 目标IRC频道节点ID
- Delay 距离该Actions被触发时的延迟

两个标签中间是要发送的消息  

## LaunchHackScript
作用:启动黑客脚本  
属性：
- Filepath 黑客脚本位置
- SourceComp 源电脑，也就是执行操作后留下日志的电脑
- TargetComp 目标电脑，黑客脚本作用的电脑
- RequireLogsOnSource 可选属性，是否目标电脑在源电脑上留下日志的情况下才启动
- RequireSourceIntact 可选属性，是否原电脑没有被清空系统文件的情况下才启动

这是一个自闭合标签，可以被延迟  

## SwitchToTheme
作用:更改玩家的主题  
属性:
- ThemePathOrName 主题的路径或者是名字
- FlickerInDuration 当切换主题时，界面闪烁的时间，单位为秒，设定为小于等于0则直接切换不闪烁

这是一个自闭合标签

## AddConditionalActions
作用:在Action中执行另一个Action  
属性:
- Filepath Action文件路径

这是一个自闭合标签

## AddAsset
作用:向指定节点添加文件  
属性:
- FileName 要添加的文件名字
- FileContents 要添加的文件的内容
- TargetComp 目标节点
- TargetFolderpath 需要添加到的路径

这是一个自闭合标签  

## StartScreenBleedEffect
作用:开启红屏效果，也就是被追踪，要ISP改IP时的效果和最后删Entech文件的效果  
属性:
- AlertTitle 红屏标题
- CompleteAction 完全红屏后执行的Action
- TotalDurationSeconds 完全红屏所用时间

两个标签中的内容为红屏后左下角的提示，最多只能有三行，可以被延迟  

## CancelScreenBleedEffect
作用:关闭红屏效果  
属性:无特殊属性  

这是一个自闭合标签，可以被延迟  

## KillExe
作用:终止某个exe进程  
属性:
- ExeName 要结束的exe名字  

这是一个自闭合标签，可以被延迟  