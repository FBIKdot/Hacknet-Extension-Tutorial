# Actions (行动)

Actions可以根据特定条件控制游戏内容. 例如DHS中的对话, DLC中Coel的破坏白名单等, 它实现游戏的各种特效, 是一个优秀的扩展不可或缺的一部分.

为了更好的去介绍Action各个标签的功能, 我们在此将Action的标签分为3大类型:
- 根标签
- 条件标签
- 行为标签

一个Action的结构大概如下:  
```xml
<!-- 根标签 -->
<ConditionalActions>

    <!-- 条件标签 -->
    <Instantly needsMissionComplete="false">

        <!-- 行为标签 -->
        <SaveGame DelayHost="delayNode" Delay="0"/>
        ...
    </Instantly>

    ...
</ConditionalActions>
```
# 根标签

Action的根标签为`<ConditionalActions>`, 无属性.

# 条件标签

Action拥有触发条件功能. 触发条件通过**条件标签**来设置.

当玩家达成触发条件后, 这个**条件标签**的**子标签**(**行为标签**)将会被执行.

条件标签必须是根标签的下一级标签.


## 所有条件标签及其属性
~~~xml
<Instantly needsMissionComplete="false"></Instantly>
~~~
`<Instantly>`: 立即触发.
- *`needsMissionComplete`: 是否要在在任务完成后触发. 这是个非必须属性, 默认为`false`

~~~xml
<OnConnect target="targetComp"></OnConnect>
~~~
`<OnConnect>`: 连接某个节点后触发.
- `target`: 需要连接的节点ID

~~~xml
<OnDisconnect target="targetComp"></OnDisconnect>
~~~
`<OnDisconnect>`: 断开某个节点后触发.
- `target`: 需要断开的节点ID

**注意:! 由于Hacknet的Bug, 如果`target`是`playerComp`, 即使没有断开玩家节点, `<OnDisconnect>`都会触发!**

~~~xml
<HasFlags requiredFlags="flag1,flag2"></HasFlags>
~~~
`<HasFlags>`: 拥有某项flag(s)后触发.
- `requiredFlags`: 需要的flag, 多个flag用英文逗号隔开.

~~~xml
<OnAdminGained target="targerComp"></OnAdminGained>
~~~
`<OnAdminGained>`: 获取某个节点的管理员权限后触发.
- `target`: 需要获取管理员权限的节点ID

~~~xml
<DoesNotHaveFlags requiredFlags="flag1,flag2">
    <!-- 没有实装, 一用就报错 -->    
</DoesNotHaveFlags>
~~~
`<DoesNotHaveFlags>`: 没有某项flag(s)后触发.
- `requiredFlags`: 需要的flag, 多个flag用英文逗号隔开. 

**没有实装, 但是出现在了官方的教程扩展`IntroExtension`里面. 一用就报错.**

# 行为标签

行为标签控制游戏内容. Action在触发条件成立后将会执行行为标签.

行为标签是条件标签的下一级标签.

行为标签可以通过功能大致分为以下部分:
- 加载类 行为标签
- 文件操作类 行为标签
- 特殊内容操作类 行为标签
- 节点操作类 行为标签
- HacknetOS操作类 行为标签

部分行为标签可以被延迟. `Action`的延迟通过DelayHost(延迟主机)实现, 此过程将会在DelayHost的`/runtime`生成缓存文件.

如果行为标签可以延迟, 并且需要延迟, 则应指定两个属性. 下文将不在逐个说明. 属性如下:
- `DelayHost`: DelayHost的ID. 因Hacknet的特性, Action的延迟功能需要一个节点帮助, 这个节点就是DelayHost. DelayHost需要拥有`FastActionHost`守护线程
- `Delay`: 延迟时间, 单位为秒

可延迟行为标签的示范代码块中均包含`DelayHost`与`Delay`属性. 

不可延迟的行为标签自身没有延迟功能, 但可以通过其他方式进行延迟, 比如使用`<AddConditionalActions>`.

***注意! 以下简称自闭和标签(空内容标签)为"空标签". 在所有可以延迟的行为标签中, 所有的`DelayHost`属性和`Delay`均为非必须属性.***
## 加载类行为标签
~~~xml
<AddConditionalActions Filepath="Actions/NextAction.xml" DelayHost="delayNode" Delay="0"/>
~~~
`<AddConditionalActions>`: 加载另一个Action
- `Filepath`: Action文件相对路径


| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

可以通过`<AddConditionalActions>`使得部分不可延迟的行为标签延迟. 

~~~xml
<LaunchHackScript Filepath="Scripts/HackerScript.txt" DelayHost="delayNode" Delay="0" SourceComp="SourceComp" TargetComp="TargetComp" RequireLogsOnSource="false" RequireSourceIntact="true"/>
~~~
`<LaunchHackScript>`: 运行HackerScript
- `Filepath`: HackerScript的相对位置
- `SourceComp`: 攻击源节点. HackerScript的攻击源节点需要设置为`[TARGET_COMP]`
- `TargetComp`: 目标节点. HackerScript的攻击源节点需要设置为`[SOURCE_COMP]`
- `RequireLogsOnSource`: 目标节点是否需要在攻击源节点上留下日志. 默认为false
- `RequireSourceIntact`: 攻击源节点是否需要系统网络文件

| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

~~~xml
<LoadMission MissionName="Missions/SurpriseMission.xml"/>
~~~
`<LoadMission>`: 立即加载任务
- `MissionName`: 任务的相对路径

| 空标签 | 延迟 |
| --- | --- |
| 是 | **否** |

~~~xml
<RunFunction FunctionName="FunctionName" FunctionValue="0" DelayHost="delayNode" Delay="0"/>
~~~
`<RunFunction>`: 运行Function
- `FunctionName`: Function的名字
- `FunctionValue`: Function运行时传递参数值. 部分Function运行需要传递参数值


| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

~~~xml
<SaveGame DelayHost="delayNode" Delay="0"/>
~~~
`<SaveGame>`: 保存游戏  

| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

## 文件操作类
~~~xml
<AddAsset FileName="FileName" FileContents="text" TargetComp="playerComp" TargetFolderpath="home"/>
~~~
`AddAsset`: 向指定节点添加文件  
- `FileName` 要添加的文件名字
- `FileContents` 要添加的文件的内容
- `TargetComp` 目标节点
- `TargetFolderpath` 文件将会存放的路径

| 空标签 | 可延迟 |
| --- | --- |
| 是 | **否** |

~~~xml
<AppendToFile DelayHost="delayNode" Delay="0" TargetComp="companyWhitelist" TargetFolderpath="Whitelist" TargetFilename="list.txt">#PLAYER_IP#</AppendToFile>
~~~
`<AppendToFile>`: 附加内容到文件.
- `TargetComp`: 目标节点.
- `TargetFolderpath`: 目标文件所在目录.
- `TargetFilename`: 目标文件名.
- 内容: 添加到内容, 将会另起一行. 可以为空.

| 空标签 | 可延迟 |
| --- | --- |
| **否** | 是 |

~~~xml
<CopyAsset DestFilePath="home" DestComp="playerComp" SourceComp="assetNode" SourceFileName="copycat.txt" SourceFilePath="home/copy"/>
~~~
`<CopyAsset>`: 文件复制
- `SourceComp`: 源节点, 即拷贝目标的节点
- `SourceFileName`: 源文件, 即拷贝目标
- `DestFilePath`: 目标路径, 即粘贴的路径
- `DestComp`: 目标节点, 即粘贴的目标节点

| 空标签 | 可延迟 |
| --- | --- |
| 是 | **否** |

~~~xml
<DeleteFile TargetComp="playerComp" FilePath="home" FileName="deleteme.txt" DelayHost="delayNode" Delay="0"/>
~~~
`<DeleteFile>`: 删除文件
- `TargetComp`: 目标节点
- `FilePath`: 文件路径
- `FileName`: 文件名

| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

## 特殊内容操作类
~~~xml
<AddIRCMessage Author="Kaguya" TargetComp="ircNode" Delay="0">text</AddIRCMessage>
~~~
`AddIRCMessage`: 向IRC中添加消息 
- `Author`: 信息的发送人
- `TargetComp`: 目标IRC频道节点ID
- `Delay`: 距离该Actions被触发时的延迟
- 内容: 消息内容  

IRC(DHS)消息的延迟发送通过目标服务器充当"`DelayHost`", 缓存内容将在IRC(DHS)的`runtime`目录生成, 无需`DelayHost`. 以下为在IRC(DHS)节点的`runtime`目录位置:
- IRC: `/IRC/runtime`
- IRCHub(DHS): `/HomeBase/runtime`

| 空标签 | 可延迟 |
| --- | --- |
| **否** | **是, 且不需要`DelayHost`** |
  
~~~xml
<SwitchToTheme ThemePathOrName="Themes/ExampleTheme.xml" FlickerInDuration="3.0" DelayHost="delayNode" Delay="0"/>
~~~
`SwitchToTheme`: 更改玩家的主题  
- `ThemePathOrName`: 主题的路径或者是名字
- `FlickerInDuration`: 当切换主题时, 界面闪烁的时间, 单位为秒, 设定为小于等于0则直接切换不闪烁

| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

~~~xml
<AddConditionalActions Filepath="Actions/NextAction.xml" DelayHost="delayNode" Delay="0"/>
~~~
`AddConditionalActions`: 在Action中执行另一个Action  
- `Filepath`: Action文件路径

| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

~~~xml
<StartScreenBleedEffect AlertTitle="Sequencer Attack" CompleteAction="Actions/ScreenBleedFailed.xml" TotalDurationSeconds="100" DelayHost="delayNode" Delay="0">Break into the Moonshine servers
Delete all files and backups
Get out of there!</StartScreenBleedEffect>
~~~
`StartScreenBleedEffect`:开启红屏效果, 也就是被追踪, 要ISP改IP时的效果和最后删Entech文件的效果
- `AlertTitle`: 红屏标题
- `CompleteAction`: 完全红屏后执行的Action
- `TotalDurationSeconds`: 完全红屏所用时间
- 内容: 红屏后左下角的提示. 最多只能有三行

需要注意的是`AlertTitle`的英文字母小写与大写在游戏中对应的字体不同.

| 空标签 | 可延迟 |
| --- | --- |
| **否** | 是 |

~~~xml
<CancelScreenBleedEffect DelayHost="delayNode" Delay="0"/>
~~~
`CancelScreenBleedEffect`: 关闭红屏效果    


| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |

~~~xml
<KillExe DelayHost="delayNode" Delay="0" ExeName="*"/>
~~~
`KillExe`: 终止某个exe进程  
- `ExeName`: 要结束的exe名字. 可以使用通配符`*`代指任意内容

| 空标签 | 可延迟 |
| --- | --- |
| 是 | 是 |