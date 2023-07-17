# Faction (阵营)

Faction相当于一部分Action的包装, 与Action的区别在于**触发条件**.

Faction只能通过`ExtensionInfo.xml`加载, 一个扩展可以加载多个Faction.

只能通过Function`setFaction`来设置玩家的Faction.

Faction通过`Rank`(排名), 又称`Point`(积分)触发, 不同Faction的`Rank`是互相独立的.

玩家可以通过相对应的`<missionHubServer>`守护进程查看用户与其对应的`Rank`数.

以下为Faction的大致结构:
~~~xml
<!-- 根标签 -->
<CustomFaction name="Faction Name" id="Faction_ID" playerVal="0">
    
    <!-- Action条件标签 -->
    <Action ValueRequired="1">

        <!--任何 Action 行为标签-->
        ...
    </Action>

    <Action ValueRequired="2">
        ...
    </Action>

</CustomFaction>
~~~

# Faction中的标签及其属性:

Faction中的标签分为3类, 分别是:
- 根标签
- Faction中的Action条件标签
- Action行为标签

## 根标签
Faction根标签`<CustomFaction>`的属性:

- `name`: Faction的名字
- `id`: Faction的id, 在设置Faction时起到作用
- `playerVal`: 玩家在该Faction的初始`Rank`

## Faction中的Action条件标签
Faction中的Action条件只有一个和Rank相关的条件

Faction中的Action条件标签`<Action>`: 
- `ValueRequired`: 激活该Action所需的`Rank`值 
- 子标签: 可以为任何Action的行动标签

## Action行为标签
第三级标签可以是任何的 [Action行为标签](./Actions.md#行为标签)