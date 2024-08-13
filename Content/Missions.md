# Missions
在Hacknet中，每个邮件都是一个Mission，同时，Entopy和CSEC的任务数据库中的任务和DHS中的任务也是Mission  
一个Mission的结构大概如下:  
```xml
<?xml version = "1.0" encoding = "UTF-8" ?>
<mission id="testMission0" activeCheck="true" shouldIgnoreSenderVerification="false">
    <goals>
        <goal type="filedeletion" target="advExamplePC" file="asdf.txt" path="home"/>
    </goals>
    <missionStart val="7" suppress="true">changeSong</missionStart>
    <missionEnd val="1">addRank</missionEnd>
    <nextMission IsSilent="false">NONE</nextMission>
    <branchMissions>
        <branch>Missions/BranchExample/TestBranchMission.xml</branch>
    </branchMissions>
    <posting title="Do the Extension Test Mission" reqs="someCustomFlag" requiredRank="3" >
content
    </posting>
    <email>
        <sender>Matt</sender>
        <subject>Test Mission Email</subject>
        <body>body</body>
        <attachments>
            <note title="An example note">note</note>
            <link comp="missionTestNode" />
        <account comp="missionTestNode" user="TestUser" pass="testpass" />
        </attachments>
    </email>
</mission>
```  
我们可以看到，Mission由`<mission>`开始，由`</mission>`结束  
在开始标签中可以定义三个属性:  
- id 任务id，必须属性
- activeCheck 是否自动检查，也就是不需要玩家手动提交
- shouldIgnoreSenderVerification 忽略发送者验证


一个mission大概有以下几个部分:  
- goals 任务完成条件
- missionStart 任务开始时执行的操作
- missionEnd 任务结束时执行的操作
- nextMission 下一个任务
- branchMissions 分支任务
- posting 用于任务数据库和DHS的额外标识
- email 给玩家发送的邮件(ps:在DHS中，不会给玩家发邮件)


## Goals
goals指的是任务完成条件，一个Mission可以有很多个goal，Matt提供的goal类型也有很多  
goal格式应为:`<goal type=[goal类型] [其余参数]/>`  
goal共有以下几个类型:  

### filedeletion
```xml
<goal type="filedeletion" target="advExamplePC" file="asdf.txt" path="home"/>
```
类型:删除文件  
参数:
- target 目标节点ID
- file 文件名
- path 文件所在目录

### clearfolder
```xml
<goal type="clearfolder" target="advExamplePC" path="home"/>
```
类型:清空文件夹  
参数:
- target 目标节点ID
- path 要清空的目录路径

### filedownload
```xml
<goal type="filedownload" target="advExamplePC" file="downloadFile.txt" path="home"/>
```
类型:下载指定文件  
参数:
- target 目标节点ID
- file 下载文件名
- path 下载文件所在目录

### filechange
```xml
<goal type="filechange" target="advExamplePC" file="changeFile.txt" path="home" keyword="extension"/>
```
类型:更改文件内容  
参数:
- target 目标节点ID
- file 目标文件
- path 目标文件所在目录
- keyword 目标内容
- removal 是否使keyword值在文件中不出现，可选参数，默认false
- caseSensitive 区分大小写，可选参数，默认false

#### 附加内容
由于该类型可能较难理解，附加内容补充，我们将举一个例子  
```xml
<goal type="filechange" target="advExamplePC" file="changeFile.txt" path="home" keyword="extension"/>
<goal type="filechange" target="advExamplePC" file="changeFile.txt" path="home" keyword="data" removal="true" caseSensitive="true"/>
```
这是一个组合goal,第一个goal指的是让关键字extension在changeFile.txt中出现  
第二个goal指的是让关键字data在文件changeFile.txt中不出现，不区分大小写  
这个组合goal可以实现:让文件中的data替换为extension  

### getadmin
```xml
<goal type="getadmin" target="advExamplePC"/>
```
类型:获取指定电脑的管理员权限  
参数:
- target 目标节点ID

### getstring
```xml
<goal type="getstring" target="password" />
```
类型:在附加内容中存在指定内容  
参数:
- target 需要与附加内容匹配的字符串

### delay
```xml
<goal type="delay" time="10.0"/>
```
类型:仅延迟一段时间  
参数:
- time 延迟时间，单位秒

### hasflag
```xml
<goal type="hasflag" target="flagName"/>
```
类型:获取指定flag  
参数:
- target 目标flag

### fileupload
```xml
<goal type="fileupload" target="advExamplePC" file="asdf.txt" path="home" destTarget="introFactionHomeNode" destPath="Drop/Uploads"/>
<goal type="fileupload" target="advExamplePC" file="asdf2.dec" path="home" destTarget="introFactionHomeNode" destPath="home" decrypt="true" decryptPass="password"/>
```
类型:上传文件  
参数:
- target 目标节点ID
- file 目标文件
- path 目标文件所在目录
- destTarget 目标文件需要上传到的节点
- destPath 目标文件需要上传到的目录
- decrypt 是否需要解密，适用于dec加密文件，可选参数，默认false
- decryptPass 指定decrypt为true后需要，解密密码，可选参数

### AddDegree
```xml
<goal type="AddDegree" owner="John Stalvern" degree="Masters in Digital Security" uni="Manchester University" gpa="3.0"/>
```
类型:在国际学术数据库中添加人员学历  
参数:
- owner 目标人名
- degree 需要添加的学位名
- uni 需要添加的学校名
- gpa 绩点

### wipedegrees
```xml
<goal type="wipedegrees" owner="John Stalvern"/>
```
类型:在国际学术数据库中删除人员数据  
参数:
- owner 目标人名

### sendemail
```xml
<goal type="sendemail" mailServer="jmail" recipient="mailuser123" subject="Email Subject!"/>
```
类型:发送邮件  
参数:
- mailServer 邮件服务器节点ID
- recipient 接受者
- subject 标题

### removeDeathRowRecord
```xml
<goal type="removeDeathRowRecord" fname="Matt" lname="Trobbiani"/>
```
类型:删除人员死亡记录  
参数:
- fname 人员First Name(名)
- lname 人员Last Name(姓)

#### 附加内容
该goal可以是一个自闭合标签，也可以在开始和结束标签中添加遗言  

### getadminpasswordstring(DLC专属)
```xml
<goal type="getadminpasswordstring" target="advExamplePC"/>
```
类型:在附加内容中填写了指定节点的管理员密码  
参数:
- target 目标节点ID


## missionStart
在任务开始时执行的内容  
可选属性:
- val 给内置函数传的参数
- suppress 是否在发送邮件时触发，否则在加载任务时触发

开始和结束标签中间是具体要执行的function(内置函数)

## missionEnd
在任务结束时执行的内容  
可选属性只有一个,val 给内置函数传的参数

开始和结束标签中间是具体要执行的function(内置函数)

## nextMission
下一个任务，也就是完成本任务后自动跳转的任务  
可选属性只有一个,IsSilent 让这个任务不发邮件安静处理，注意是当前任务不是下一个任务

开始和结束标签中间是下一个Mission的相对路径，可以为NONE

## branchMissions
分支任务  
解释:如果完成了分支任务中任何一个任务的所有goal，则自动跳转到该分支任务的nextMission  
branchMissions中可以有多个mission  
实例格式:  
```xml
<branchMissions>
    <branch>Missions/BranchExample/TestBranchMission.xml</branch>
</branchMissions>
```

## posting
用于在任务数据库和DHS中添加额外内容  
属性:
- title 显示的标题
- reqs 解锁该任务需要的flag
- requiredRank 解锁该任务需要的积分

开始标签和结束标签中间为显示的该任务大致描述

## email
给玩家发送的邮件，若为DHS任务则不发送邮件  
可用标签:
- sender 发送者
- subject 标题
- body 内容，同时也可以是DHS任务中的任务详情

### attachments
邮件附件  
可用标签:  

#### note
笔记，属性:
- title 在邮件中显示的标题

开始标签和结束标签中间为笔记内容

#### link
节点链接，属性:
- comp 目标节点ID

这是一个自闭合标签

#### account
账号，属性:
- comp 目标节点ID
- user 用户名
- pass 密码
