# 新增 Hacknet ExtensionInfo.xml 使用文档

## 概述

ExtensionInfo.xml是Hacknet扩展的核心配置文件，定义了扩展的基本属性、启动设置、资源引用等关键信息。

## 基本结构

```xml
<HacknetExtension>
  <!-- 配置项 -->
</HacknetExtension>
```

## 主要配置项详解

### 1. 语言设置
```xml
<Language>zh-cn</Language>
```
- 设置扩展的语言
- 支持的语言：英语(en-us)、德语(de-de)、法语(fr-be)、俄语(ru-ru)、西班牙语(es-ar)、韩语(ko-kr)、日语(ja-jp)、简体中文(zh-cn)

### 2. 基本信息
```xml
<Name>IntroExtension</Name>
<AllowSaves>true</AllowSaves>
```
- **Name**: 扩展名称（最大128字符，注意：不能是中文）
- **AllowSaves**: 是否允许保存游戏进度

### 3. 启动设置
```xml
<StartingVisibleNodes>advExamplePC</StartingVisibleNodes>
<StartingMission>Missions/Intro/IntroMission1.xml</StartingMission>
<StartingActions>Actions/StartingActions.xml</StartingActions>
```
- **StartingVisibleNodes**: 初始可见节点（逗号分隔）
- **StartingMission**: 玩家启动时加载的任务
- **StartingActions**: 新会话创建时加载的条件动作集

### 4. 描述信息
```xml
<Description>——介绍扩展——
这个示例扩展将教授构建Hacknet扩展的基础知识。
描述可以是多行，所以，我们已经在学习了!</Description>
```
- 在Hacknet中显示的扩展描述
- 支持多行文本

### 5. Faction设置
```xml
<Faction>Factions/ExampleFaction.xml</Faction>
<Faction>Factions/IntroFaction.xml</Faction>
```
- 定义扩展中涉及的阵营
- 可以定义任意数量的阵营

### 6. 教程和启动设置
```xml
<StartsWithTutorial>False</StartsWithTutorial>
<HasIntroStartup>true</HasIntroStartup>
```
- **StartsWithTutorial**: 是否以教程开始
- **HasIntroStartup**: 是否使用标准重启启动序列

### 7. 主题和音乐
```xml
<StartingTheme>Themes/ExampleTheme.xml</StartingTheme>
<IntroStartupSong>The_Quickening</IntroStartupSong>
```
- **StartingTheme**: 初始主题文件路径
- **IntroStartupSong**: 启动音乐（原版游戏歌曲名或自定义.ogg文件路径）

### 8. 扩展序列器设置 （主线末尾的Sequencer.exe）
```xml
<SequencerTargetID>advExamplePC</SequencerTargetID>
<SequencerSpinUpTime>10.5</SequencerSpinUpTime>
<SequencerFlagRequiredForStart>testFlag</SequencerFlagRequiredForStart>
<ActionsToRunOnSequencerStart>Actions/ThemeSwapActions.xml</ActionsToRunOnSequencerStart>
```
- **SequencerTargetID**: 序列器目标计算机ID
- **SequencerSpinUpTime**: 序列器启动时间（秒）
- **SequencerFlagRequiredForStart**: 启动序列器所需的Faction（派系，如：CSEC）Flag（一种标签，可在mission中添加）
- **ActionsToRunOnSequencerStart**: 序列器启动时运行的Action（动作）文件

### 9. Steam Workshop设置
```xml
<WorkshopDescription>扩展描述（最多8000字符）</WorkshopDescription>
<WorkshopLanguage>English</WorkshopLanguage>
<WorkshopVisibility>2</WorkshopVisibility>
<WorkshopTags>Extension</WorkshopTags>
<WorkshopPreviewImagePath>WorkshopLogo.png</WorkshopPreviewImagePath>
<WorkshopPublishID>NONE</WorkshopPublishID>
```
- **WorkshopDescription**: Steam Workshop描述
- **WorkshopLanguage**: Workshop语言
- **WorkshopVisibility**: 可见性（0=公开，1=仅好友，2=私有）
- **WorkshopTags**: 标签（逗号分隔）
- **WorkshopPreviewImagePath**: 预览图片路径（必须为正方形，小于1MB）
- **WorkshopPublishID**: 发布ID（首次发布后自动填充）

## 使用建议

1. **路径引用**: 所有文件路径都相对于扩展根目录
2. **音乐文件**: 可以引用原版游戏音乐或自定义.ogg文件
3. **主题文件**: 支持基础主题名称或自定义主题文件
4. **Workshop发布**: 首次发布前WorkshopPublishID应为"NONE"

## 示例配置

```xml
<HacknetExtension>
  <Language>zh-cn</Language>
  <Name>myext</Name>
  <AllowSaves>true</AllowSaves>
  <StartingMission>Missions/MyMission.xml</StartingMission>
  <Description>这是我的第一个Hacknet扩展</Description>
  <Faction>Factions/MyFaction.xml</Faction>
  <StartingTheme>Themes/MyTheme.xml</StartingTheme>
</HacknetExtension>
```

## 文件结构参考
