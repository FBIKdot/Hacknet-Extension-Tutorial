# Faction (阵营)

Faction相当于一部分Action的包装, 与Action的区别在于**触发条件**.

Faction只能通过`ExtensionInfo.xml`加载, 一个扩展可以加载多个Faction.

Faction通过`Rank`(等级), 又称`Point`(积分)触发, 不同Faction的`Rank`是互相独立的.

以下为Faction的大致结构:
~~~xml
<CustomFaction name="Faction Name" id="Faction_ID" playerVal="0">
    <Action ValueRequired="1">
        ...
    </Action>

    <Action ValueRequired="2">
        ...
    </Action>
</CustomFaction>
~~~

Faction根标签`<CustomFaction>`的属性:

- `name`: Faction的名字
- `id`: Faction的id, 在设置Faction时起到作用.
- `playerVal`: 玩家在该Faction的初始`Rank`.

# Faction的标签及其属性:

Action标签`<Action>`: 
- `ValueRequired`: 激活该Action所需的`Rank`值. 
- 子标签: 可以为任何Action的行动标签.