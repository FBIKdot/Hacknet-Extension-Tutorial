# Extension

扩展内容通过类型可以大致分为11个部分, 这些部分别是:  
- [Actions](./Actions.md) (行为) 实现游戏中的各种操作, 各种对话, 各种特效等  
- [Factions](./Faction.md) (阵营) 是特殊的Action, 可实现比如CSEC任务数据库中最后一个任务的锁定  
- [HackerScripts](./HackerScripts.md) 黑客脚本, 用来描述黑客行为  
- Missions (任务) 声明了玩家的"任务". 在Hacknet中, 每一个邮件都是一个"任务".  
- Docs 特殊的"Mission". 一些文本内容, 如el论坛的帖子. 
- Music (音乐) 音乐资源, 如BGM.
- Nodes (节点) 用于声明扩展中存在的节点.
- People (人) 用于在通用医疗, 国际学术数据库和死亡人员数据库中添加人员数据
- Themes (主题) 扩展自定义的Theme, 也就是x-server.sys
- Web (网页) 用于Web服务器节点的html,css文件等  

虽然有11个类型, 但实际上, 只有Actions,Factions,Missions,HackerScripts和Nodes关系到游戏行为, 其余均为资源. 
