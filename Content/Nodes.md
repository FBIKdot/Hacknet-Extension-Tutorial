# Nodes
## 基本信息
Nodes,节点,是Hacknet中重要的一部分,玩家电脑,DHS,任务数据库,eos设备都属于Nodes  
一个Nodes的结构大概如下:  
```xml
<?xml version = "1.0" encoding = "UTF-8" ?>
<Computer id="advExamplePC" 
          name="Extension Example PC" 
          ip="167.194.132.7"
          security="2"
          allowsDefaultBootModule="false"
          icon="chip" 
          type="1" > 
    <adminPass pass="password" />
    <account username="Matt" password="testpass" type="ALL" />
    <ports>21, 22, 25, 80, 1433, 104, 6881, 443, 192, 554</ports>
    <portsForCrack val="0" />
    <trace time="5678" />
    <admin type="fast" resetPassword="false" isSuper="false"/> 
    <dlink target="advExamplePC2" />
    <file path="home" name="Test_File.txt">This is a test file in the home directory</file>
</Computer>
```  
PS:第一行用于指定xml的版本和编码,在本教程中忽略,虽然在Node中不写这一行好像没有什么影响,但我们仍然建议写上这一行  

我们可以看到,一个Node由`<Computer>`开始,并在该标签中指定一些属性,由`</Computer>`结束  

Computer标签可以指定的属性有:
- `id` 节点ID,在Hacknet中需要为唯一
- `name` 节点的显示名称,可以不唯一
- `ip` 可选属性,硬编码该Node的ip地址
- `security` 安全等级
- `allowsDefaultBootModule` 可选属性,是否允许默认的启动模块(见下文)
- `icon` 可选属性,节点的显示图标
- `type` 可选属性,节点类型(用来指定生成垃圾信息,指定为1,2,3效果一样),可为:1(企业),2(家庭电脑),3(服务器),4(空,不生成垃圾IRC信息),5(当作eos设备,会生成eos设备相关文件)等等

### allowsDefaultBootModule
每个Node可以有一个或多个(或没有)**daemon**,daemon实现了如DHS,白名单,任务数据库这样的在Node上运行的程序  

我们在游玩Hacknet本体或DLC时,总是一连接Node就会自动显示它的daemon(如啃得鸡服务器,CSEC任务数据库等) 

该属性就用来控制这种特性,当`allowsDefaultBootModule`被指定为true时,玩家一旦连接该Node就会显示该Node所定义的最后一个daemon  

若该属性被指定为false,则连接到该Node时会显示该节点的信息概览(登录,扫描系统,查看文件系统,扫描网络)而不会自动转到该Node所运行的daemon

### icon
节点的icon可以有:
- `laptop` 便携笔记本
- `chip` 心脏起搏器那种看起来像硬件的图标
- `kellis` 原版Kellis服务器的图标(通用医疗)
- `tablet` 平板
- `ePhone` eos设备(黑色)
- `ePhone2` eos设备(白色)

DLC专属:
- `Psylance` Psylance的帽子图标
- `PacificAir` 飞机图标
- `Alchemist` 炼金术师任务的大树图标

这里还有一些描述不太清楚的,附上图片:  

`DLCLaptop`：  
![](../Assets/Nodes/Icon_DLCLaptop.png)

`DLCPC1`：  
![](../Assets/Nodes/Icon_DLCPC1.png)

`DLCPC2`:  
![](../Assets/Nodes/Icon_DLCPC2.png)

`DLCServer`:  
![](../Assets/Nodes/Icon_DLCServer.png)

### security
Node的security指定Node的安全等级

在没有覆写Node的属性时:  
当security为1-3时,仅需破解端口即可入侵  
当security为4或以上时,会自动添加:自动重置密码,代理和防火墙  
可以重定义这些属性  

## 其他属性
在`<Computer>` 与 `</Computer>` 中可以定义Node的其他属性  

下面是关于其他属性的详细信息:

### adminPass
```xml
<adminPass pass="password" />
```
硬编码该Node的管理员密码  
`pass` : 管理员密码  

### account
```xml
<account username="Matt" password="testpass" type="ALL" />
```
为该Node额外添加一个帐号,可以通过重复定义该属性添加多个帐号  
`username` : 添加的帐号名  
`password` : 添加的帐号密码  
`type` : 帐号类型  

帐号类型有:
- `ADMIN` =0,管理员权限
- `ALL` =1,有对文件的操作权限,但不能使用扫描网络等需要管理员权限的操作
- `MAIL` =2,邮件帐号
- `MISSIONLIST` =3,类似于CSEC的任务数据库帐号

你可以使用对应的数字或者直接填写类型来定义帐号类型

### ports
```xml
<ports>21, 22, 25, 80, 1433, 104, 6881, 443, 192, 554</ports>
```
定义该Node开放的端口  

端口在`<port>` 与 `</port>` 中定义,以英文逗号隔开,空格可以省略

默认情况下,可用的端口有:
- `21` ftp端口
- `22` ssh端口
- `25` smtp端口
- `80` web端口
- `1433` sql服务器端口
- `104` KBT端口
- `6881` DLC特供,torrent端口
- `443` DLC特供,ssl(https)端口
- `192` DLC特供,Pacific飞机端口
- `554` DLC特供,原版中未出现,RTSP端口(使用RTSPCrack破解)

### proxy
```xml
<proxy time="2" />
```
为该Node定义代理,覆盖`security`的自带代理  
`time` : 过载所需时间,乘以30为实际过载所需秒数,设置为-1禁用代理

### portsForCrack
```xml
<portsForCrack val="0" />
```
定义Node破解所需端口数  
`val` : 破解所需的端口数,设置为101以上会启用EnSec(那个红条,无法porthack的)

### firewall
```xml
<firewall level="6" solution="Scypio" additionalTime="1.0"/>
```
定义Node的防火墙属性,可以覆盖`security`的自带代理  
`level` : 防火墙等级,即破解口令的字符数量,设置为-1禁用防火墙  
`solution` : 破解口令  
`additionalTime` : 可选参数,分析每一级需要的时间,单位为秒

### admin
```xml
<admin type="fast" resetPassword="false" isSuper="false"/> 
```

用于实现玩家断开时重置代理,端口等特性  
`type` : 管理员类型  
`resetPassword` : 是否在断开时重置密码  
`isSuper` : 是否为超级管理员  

可用的管理员类型有:
- `basic` : 断开15秒后重置端口破解状态
- `progress` : 在玩家非管理员情况下可重置端口破解状态和代理,防火墙破解状态
- `fast` : 与`isSuper`配合,断开时立即重置管理员密码

示例:  
```xml
<admin type="fast" resetPassword="true" isSuper="true"/>
```
断开连接后立即重置管理员密码  

```xml
<admin type="progress"/>
```
在玩家非管理员状态下,断开连接后重置所有入侵状态,建议一般节点定义此属性  

```xml
<admin type="none"/>
```
不使用该特性,可以用来禁用由`security`大于等于4带来的自动重置特性

### portRemap
```xml
<portRemap>web=1234,22=2</portRemap>
```
端口映射,即实现类似DLC中端口非默认的效果  
在`<portRemap>` 与 `</portRemap>` 中定义,以`原端口=目标端口`定义,英文逗号隔开  

原端口既可以写端口号,也可以是端口名称  

如本例中,将web服务器端口重定向为1234,将22端口重定向为2  

可用的端口名称有:
- `ssh` ssh端口(22)
- `ftp` ftp端口(21)
- `web` web端口(80)
- `torrent` DLC特供,torrent端口(6881)
- `medical` KBT端口(104)
- `smtp` smtp端口(25)
- `sql` sql数据库端口(1433)

### tracker
```xml
<tracker />
```
为该Node启用被动追踪  

被动追踪,指若玩家在该Node上留下了下载或删除文件的日志,就会受到AI自动攻击(forkbomb)  

若存在CSEC_Member的flag,则玩家会受到类似CCC黑客小队的红屏攻击  

### dlink
```xml
<dlink target="advExamplePC2" />
```
定义该Node被scan后可以扫出的节点,可以通过重复定义该属性添加多个可以扫描到的节点  

`target` : 连接的节点ID

### positionNear
```xml
<positionNear target="advExamplePC2" position="1" total="3" extraDistance="0.1" force="false"/>
```
定义该Node距离其他某个Node的距离  
//FIXME

### file
```xml
<file path="home" name="Test_File.txt">This is a test file in the home directory</file>
```
在该Node中添加文件  

`path` : 文件路径  
`name` : 文件名

在`<file>` 与 `</file>` 标签中定义文件内容

PS:文件内容支持多行,可以使用**自替换占位符**

### customthemefile
```xml
<customthemefile path="sys" name="Custom_x-server.sys" themePath="Themes/SecondaryTheme.xml"/>
```  
向Node中添加自定义的主题文件(x-server.sys)  
`path` : 主题文件的存放路径  
`name` : 主题文件名  
`themePath` : 该自定义主题的定义在扩展根目录的相对路径  

### encryptedFile
```xml
<encryptedFile path="home" name="asdf2.dec" ip="192.168.1.1" header="This is the header" pass="password">
    This is an encrypted file referenced in ExampleMission.xml
  </encryptedFile>
```  
向Node中添加DEC加密文件  
`path` : 加密文件路径  
`name` : 加密文件名  
`ip` : DECHead.exe扫出的头信息IP  
`header` : DECHead.exe扫出的头信息  
`pass` : 可选属性,定义该文件的密码  

可在`<encryptedFile>` 与 `</encryptedFile>` 中添加加密文件内容,可使用**自替换占位符**  

### eosDevice
```xml
<eosDevice name="Deliliah's ePhone 4S" id="eosIntroPhone" icon="ePhone2" empty="true" passOverride="notAlpine">
    <note>TestNote
More text</note>
    <note>Note filenames
Note filenames are generated automatically by taking the first line of the file
(in this case "Note Filenames") and replacing spaces with underscores.</note>
    <mail username="test@jmail.com" pass="thisIstheaccountpass" />
    <mail username="test2@jmail.com" pass="YouCanHaveLotsOfThese" />
    <file path="eos/test" name="crackedFile.txt">This is mostly useful for jailbroken phones</file>
  </eosDevice>
```  
为该Node添加连接的eos设备,可以通过重复定义该属性添加多个eos设备  

`name` : eos设备名  
`id` : eos设备ID,相当于节点ID  
`icon` : eos设备图标,和节点图标定义一致  
`empty` : 是否生成垃圾文件  
`passOverride` : 可选属性,重新定义该eos设备的管理员密码(默认为alpine)  

可在`<eosDevice>` 与 `</eosDevice>` 中定义该eos设备的属性  

eos设备可以定义的属性有:
#### note
```xml
<note>TestNote
More text</note>
```
添加笔记(/eos/Note中)  
第一行为笔记的标题(在/eos/Note中的文件名)  
从第二行开始为笔记正文  

#### mail
```xml
<mail username="test@jmail.com" pass="thisIstheaccountpass" />
```  
添加邮箱帐号,重复定义以添加多个邮箱帐号  
`username` : 邮箱地址  
`pass` : 邮箱密码  
PS:仍需要在目标邮件服务器中添加邮箱帐号  

#### file
用法与普通Node相同,省略

## Daemons
//TODO