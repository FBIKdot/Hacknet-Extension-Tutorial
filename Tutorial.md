# Hacknet-Extension-Tutorial-Content

## 前言  
Hacknet目前有很多的扩展，其中优秀的也有很多，比如ZQG的OCA,Kwiper的Heartbeat；还有一些比较烂的，比如Death by Bit和Real World  
但不管怎样，他们都尝试了编写自己的扩展，尝试为Hacknet社区出一份力  
目前也有很多的人想要写扩展，可国内资料匮乏，国外缺少翻译，这是一大问题  
为了解决这个问题，我们创建了这个仓库，用来尝试着完善教程，我们知道这会很难，但我们愿意尝试。

## 正文 
好，那么这里，我们就开始正式地开始此教程  
本教程通过扩展目录结构分为11个部分，这些目录分别是:  
- Actions 实现游戏中的各种操作，各种对话，各种特效等  
- Factions 多个Action的集合，可实现比如CSEC任务数据库中最后一个任务的锁定  
- Docs 一些文本内容，如el论坛的帖子  
- HackerScripts 黑客脚本，用来实现例如原版中naix的反击等  
- Missions 任务，在Hacknet中，每一个邮件都是一个任务  
- Music 扩展的音乐资源
- Nodes 扩展中存在的节点定义
- People 人口，用于在通用医疗，国际学术数据库和死亡人员数据库中添加人员数据
- Themes 扩展自定义的Theme，也就是x-server.sys
- Web 用于Web服务器节点的html,css文件等  

虽然存在11个文件夹，但实际上，只有Actions,Factions,Missions,HackerScripts和Nodes存在扩展代码，其余均为资源  
Docs，Music，People，Themes，Web不会单独拿出来单独讲解，仅在其他的代码编写中需要时提及  

### Actions
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

#### AddIRCMessage
作用:在指定IRC频道发送消息  
属性:  
- Author 信息的发送人
- TargetComp 目标IRC频道节点ID
- Delay 距离上一次执行后的延迟

两个标签中间是要发送的消息  

#### LaunchHackScript
作用:启动黑客脚本  
属性：  
- Filepath 黑客脚本位置
- DelayHost 用来给Action延迟，因Hacknet的特性，Action延迟需要一个节点帮助，这个节点就是DelayHost,需要有FastActionHost守护线程，该属性为节点ID
- Delay 距离上一次执行后的延迟，如果不需要延迟则不用指定DelayHost
- SourceComp 源电脑，也就是执行操作后留下日志的电脑
- TargetComp 目标电脑，黑客脚本作用的电脑
- RequireLogsOnSource 可选属性，是否目标电脑在源电脑上留下日志的情况下才启动
- RequireSourceIntact 可选属性，是否原电脑没有被清空系统文件的情况下才启动

这是一个自闭合标签

#### SwitchToTheme
作用:更改玩家的主题  
属性:  
- ThemePathOrName 主题的路径或者是名字
- FlickerInDuration 当切换主题时，界面闪烁的时间，单位为秒，设定为小于等于0则直接切换不闪烁

这是一个自闭合标签

#### AddConditionalActions
作用:在Action中执行另一个Action  
属性:  
- Filepath Action文件路径

这是一个自闭合标签

#### AddAsset
作用:向指定节点添加文件  
属性:  
- FileName 要添加的文件名字
- FileContents 要添加的文件的内容
- TargetComp 目标节点
- TargetFolderpath 需要添加到的路径

这是一个自闭合标签


#### StartScreenBleedEffect
作用:开启红屏效果，也就是被追踪，要ISP改IP时的效果和最后删Entech文件的效果  
属性:  
- AlertTitle 红屏标题
- CompleteAction 完全红屏后执行的Action
- TotalDurationSeconds 完全红屏所用时间
- DelayHost 中继节点，解释和上文相同
- Delay 距离上一个执行后的延迟，如果不需要延迟则不用指定DelayHost

两个标签中的内容为红屏后左下角的提示，最多只能有三行

#### CancelScreenBleedEffect
作用:关闭红屏效果
属性:  
- DelayHost 和上文相同
- Delay 和上文相同

这是一个自闭合标签  

#### KillExe
作用:终止某个exe进程  
属性:  
- DelayHost 解释和上文相同
- Delay 解释和上文相同
- ExeName 要结束的exe名字

这是一个自闭合标签  

