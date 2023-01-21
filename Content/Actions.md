# Actions (行动)

Actions可以根据特定条件控制游戏内容. 例如DHS中的对话, DLC中Coel的破坏白名单等, 它实现游戏的各种特效, 是一个优秀的扩展不可或缺的一部分.
  
为了更好的去介绍Action各个标签的功能, 我们在此将Action的标签分为3大类型:
- 根标签
- 条件标签
- 行为标签

一个Action的结构大概如下:  
```xml
<ConditionalActions>
    <!--这里是Action的其他代码-->
</ConditionalActions>
```
# 根标签

Action的根标签为`<ConditionalActions>`, 无属性.

# 条件标签

Action拥有触发条件功能. 触发条件通过**条件标签**来设置.

当玩家达成触发条件后, 这个**条件标签**的**子标签**(**行为标签**)将会被执行.

条件标签必须是根标签的下一级标签.

## 条件标签的通用非必须属性

这些触发条件都有一些通用的可选属性:  
- needsMissionComplete 当完成当前任务时触发
- requiredFlags 拥有特定flag触发

## 所有条件标签及其必须属性

`<Instantly>` 立即触发:
- 无必须属性

`<OnConnect>` 连接某个节点后触发:
- `target`: 需要连接的节点ID

`<OnDisconnect>` 断开某个节点后触发.
- `target`: 需要断开的节点ID

`<HasFlags>` 拥有某项flag(s)后触发.
- `requiredFlags`: 需要的flag, 多个flag用英文逗号隔开.

`<DoesNotHaveFlags>`没有某项flag(s)后触发.
- `requiredFlags`: 需要的flag, 多个flag用英文逗号隔开.

`<OnAdminGained>` 获取某个节点的管理员权限后触发.
- `target`: 需要获取管理员权限的节点ID

# 行为标签

行为标签控制游戏内容. Action在触发条件成立后将会执行行为标签

行为标签是条件标签的下一级标签.

部分行为标签可以被延迟. 如果需要延迟, 则应指定两个属性:
- `DelayHost`: DelayHost的ID. 因Hacknet的特性, Action的延迟功能需要一个节点帮助, 这个节点就是DelayHost. DelayHost需要拥有`FastActionHost`守护线程.
- `Delay`: 延迟时间, 单位为秒

行为标签可以通过功能大致分为以下部分:
- 加载类 行为标签
- 文件操作类 行为标签
- 特殊文件操作类 行为标签
- 节点操作类 行为标签
- HacknetOS操作类 行为标签

## 加载类行为标签

`<AddConditionalActions>`: 加载另一个Action.
~~~xml
<AddConditionalActions Filepath="Actions/NextAction.xml" DelayHost="delayNode" Delay="0"/>
~~~
- `Filepath`: Action文件相对路径.

`<RunFunction>`: 运行Function.
~~~xml
<RunFunction FunctionName="FunctionName" FunctionValue="0" DelayHost="delayNode" Delay="0"/>
~~~
- `FunctionName`: Function的名字.
- `FunctionValue`: Function运行时的参数值. 部分Function运行需要参数值.

`<LaunchHackScript>`: 运行HackerScript.
~~~xml
<LaunchHackScript Filepath="Scripts/HackerScript.txt" DelayHost="delayNode" Delay="0" SourceComp="SourceComp" TargetComp="TargetComp" RequireLogsOnSource="false" RequireSourceIntact="true"/>
~~~
- `Filepath`: HackerScript的相对位置
- `SourceComp`: 攻击源节点. HackerScript的攻击源节点需要设置为`[TARGET_COMP]`.
- `TargetComp`: 目标节点. HackerScript的攻击源节点需要设置为`[SOURCE_COMP]`.
- `RequireLogsOnSource`: 目标节点是否需要在攻击源节点上留下日志. 默认为false.
- `RequireSourceIntact`: 攻击源节点是否需要系统网络文件

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
- SourceComp 源电脑, 也就是执行操作后留下日志的电脑
- TargetComp 目标电脑, 黑客脚本作用的电脑
- RequireLogsOnSource 可选属性, 是否目标电脑在源电脑上留下日志的情况下才启动
- RequireSourceIntact 可选属性, 是否原电脑没有被清空系统文件的情况下才启动

这是一个自闭合标签, 可以被延迟  

## SwitchToTheme
作用:更改玩家的主题  
属性:
- ThemePathOrName 主题的路径或者是名字
- FlickerInDuration 当切换主题时, 界面闪烁的时间, 单位为秒, 设定为小于等于0则直接切换不闪烁

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
作用:开启红屏效果, 也就是被追踪, 要ISP改IP时的效果和最后删Entech文件的效果  
属性:
- AlertTitle 红屏标题
- CompleteAction 完全红屏后执行的Action
- TotalDurationSeconds 完全红屏所用时间

两个标签中的内容为红屏后左下角的提示, 最多只能有三行, 可以被延迟  

## CancelScreenBleedEffect
作用:关闭红屏效果  
属性:无特殊属性  

这是一个自闭合标签, 可以被延迟  

## KillExe
作用:终止某个exe进程  
属性:
- ExeName 要结束的exe名字  

这是一个自闭合标签, 可以被延迟  