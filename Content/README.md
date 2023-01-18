# Hacknet-Extension-Tutorial-Content

## 前言  
Hacknet目前有很多的扩展，其中优秀的也有很多，也有一些比较烂的  
但不管怎样，他们都尝试了编写自己的扩展，尝试为Hacknet社区出一份力  
目前也有很多的人想要写扩展，可国内资料匮乏，国外缺少翻译，这是一大问题  
为了解决这个问题，我们创建了这个仓库，用来尝试着完善教程，我们知道这会很难，但我们愿意尝试。

## Get Started  
好，那么这里，我们就正式地开始此教程  
本教程通过扩展目录结构分为11个部分，这些目录分别是:  
- [Actions](./Actions.md) 实现游戏中的各种操作，各种对话，各种特效等  
- Factions 多个Action的集合，可实现比如CSEC任务数据库中最后一个任务的锁定  
- Docs 一些文本内容，如el论坛的帖子  
- [HackerScripts](./HackerScripts.md) 黑客脚本，用来实现例如原版中naix的反击等  
- Missions 任务，在Hacknet中，每一个邮件都是一个任务  
- Music 扩展的音乐资源
- Nodes 扩展中存在的节点定义
- People 人口，用于在通用医疗，国际学术数据库和死亡人员数据库中添加人员数据
- Themes 扩展自定义的Theme，也就是x-server.sys
- Web 用于Web服务器节点的html,css文件等  

虽然存在11个文件夹，但实际上，只有Actions,Factions,Missions,HackerScripts和Nodes存在扩展代码，其余均为资源  
Docs，Music，People，Themes，Web不会单独拿出来单独讲解，仅在其他的代码编写中需要时提及  
