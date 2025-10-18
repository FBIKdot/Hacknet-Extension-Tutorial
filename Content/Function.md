# Function (函数)

Function可以更改游戏内容. 它可以在Mission和Action(包括Faction)中被执行. 

在游戏中, 作者通过Function来简化他自己对游戏的控制, 与操作特殊功能. 其中只有部分Function是可以在扩展中使用的. 

作者通过一个奇葩的方式来给Function传递参数, 这里通过`<missionStart>`和行为标签`<RunFunction>`对`setFaction`和`addRank`函数来做示范:

函数的参数必须为字符串, 则这么执行函数:
~~~xml
<missionStart>setFaction:Entropy</missionStart>
~~~
~~~xml
<RunFunction FunctionName="setFaction:Entropy"/>
~~~
假如函数的参数必须为整数, 则这么执行函数:
~~~xml
<missionStart val="1">addRank</missionStart>
~~~
~~~xml
<RunFunction FunctionName="addRank" FunctionValue="1"/>
~~~

你可以通过这样来理解: 第一个示范写成`Javascript`是这样的
~~~js
setFaction.Entropy();
~~~
第二个是
~~~js
addRank(1);
~~~


# 可用Function大全

## Faction相关Function


~~~
setFaction:FACTION_ID
~~~
设置Faction:
- `FACTION_ID`: Faction的ID.
~~~
addRank
~~~
增加Rank并发送通知邮件:
- 参数值: 增加的Rank数. 必须是个整数. 
注意! 若玩家无Faction, 该操作将失败.

~~~
addRankSilent
~~~
增加Rank但不发通知邮件:
- 参数值: 增加的Rank数. 必须是个整数.
注意! 若玩家无Faction, 该操作将失败.

~~~
addRankFaction:FACTION_ID
~~~
为指定Faction增加Rank:
- `FACTION_ID`: Faction的ID.
- 参数值: 增加的Rank数. 必须是个整数. 

## 状态操作类Function

~~~
addFlags:flagname,...
~~~
添加Flag(s):
- `flagname`: Flag的名字, 多个Flags通过英文逗号隔开.

~~~
removeFlags:flagname,...
~~~
删除Flag(s):
- `flagname`: Flag的名字, 多个Flags通过英文逗号隔开.

~~~
loadConditionalActions:PATH_TO_ACTION
~~~
加载Action:
- `PATH_TO_ACTION`: Action的相对路径.

## 系统操作类Function

~~~
flashUI
~~~
让UI闪一下.

~~~
changeSong
~~~
根据参数值更换音乐:
- 参数值: 音乐的编号.
    - 1: Revolve
    - 2: The_Quickening
    - 3: TheAlgorithm
    - 4: Ryan3
    - 5: Bit(Ending)
    - 6: Rico_Puestel-Roja_Drifts_By
    - 7: out_run_the_wolves
    - 8: Irritations
    - 9: Broken_Boy
    - 10: Ryan10
    - 11: tetrameth
  
~~~
playCustomSong:PATH_TO_SONG
~~~
淡入播放自定义音乐:
- `PATH_TO_SONG`:音乐文件的相对路径. 音乐必须是`ogg`格式.

~~~
playCustomSongImmediatley：[PATH_TO_SONG]
~~~
立即播放自定义音乐:
- `PATH_TO_SONG`:音乐文件的相对路径. 音乐必须是`ogg`格式.

## Labyrinths(DLC)独有Function
~~~
changeSongDLC
~~~
根据参数值更换Labyrinths(DLC)的音乐:
- 参数值: Labyrinths(DLC)音乐的编号.
    - 1: Remi2
    - 2: snidelyWhiplash
    - 3: Slow_Motion
    - 4: World_Chase
    - 5: HOME_Resonance
    - 6: Remi_Finale
    - 7: RemiDrone
    - 8: DreamHead
    - 9: Userspacelike
    - 10: CrashTrack

~~~
defAttackAircraft
~~~
炸飞机. 如果Node ID为`dair_crash`的节点具有`<AircraftDaemon>`守护进程, 则将它的`FlightSystems/747FlightOps.dll`文件删除并且重载固件. 

注意! 这个Function执行后会在Terminal报错, 但是该错误不会影响游戏. 你可以通过`cleanTerminal`将报错清除.