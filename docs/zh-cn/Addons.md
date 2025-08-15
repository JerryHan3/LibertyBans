
LibertyBans以扩展程序的形式提供了一些额外功能。

安装扩展不会造成额外的性能开销：它们会直接注入LibertyBans的核心，而无需经过任何中间层。以扩展的形式实现功能是保持插件可持续开发的一种设计考量。

## 安装扩展

你可以简单地使用 `/libertybans addon install <addon>` 来安装扩展。请把 `<addon>` 替换成你想要使用的扩展的ID。命令执行时，会把所需的扩展释放到文件系统中，这样下次重启的时候就可以加载了。

你也可以下载扩展jar文件，并把它放到 `plugins/LibertyBans/addons`目录中，最后重启服务器来安装扩展。

已安装扩展的数量会在启动时显示出来：
```
[LibertyBans] Detected 2 addon(s)
```

## 配置、管理扩展

扩展的配置文件和扩展jar文件的位置相同——它们都在LibertyBans插件文件夹的`addons`目录中。

在配置完扩展之后，请运行`/libertybans reload`。

# 可用的扩展

每个扩展的ID都在[中括号]中呈现。

## 添加新命令

### 检查处罚记录 [command-checkpunish]

此扩展启用了`/libertybans checkpunish <id>`命令。该命令可以根据提供的处罚ID显示一次处罚操作的具体信息。

命令需要权限`libertybans.addon.checkpunish.use`。

### 检查用户 [command-checkuser]

此扩展提供了`/libertybans checkuser <player>`命令。该命令会显示指定玩家被封禁或禁言的情况。

命令需要权限`libertybans.addon.checkuser.use`。

### 清除 [command-expunge]

此扩展提供了`/libertybans expunge <id> command`命令。该命令可以从数据库中移除指定的处罚记录。适用于清理无效或意外的处罚。

**警告：被清理的记录不可恢复。**

命令需要权限`libertybans.addon.expunge.use`。

### 延期 [command-extend]

此扩展提供了`/libertybans extend <id> <time>`命令。您可以指定一个现有且未过期的处罚，将其额外延长一定时间。

命令需要权限`libertybans.addon.extend.use`。

### 管理操作回滚 [command-staffrollback]

此扩展提供了`/libertybans staffrollback <operator> [time]`命令。执行回滚操作会彻底清除特定管理人员执行的全部处罚。适用于管理恶意处罚或者账号遭窃的情况。

`[time]`参数确定了多久之前的处罚操作应该被清除。早于该时间段的处罚操作仍会被保留。

确定了多久之前的惩罚应该被清除。**警告：被清理的记录不可恢复。**

命令需要权限`libertybans.addon.staffrollback.use`。

## Exemption 豁免

豁免功能允许你保护部分玩家不被处罚。比如，你可能想要阻止协管封禁正式管理员，并且你绝不会想要让服主被封禁。

LibertyBans允许你做到这一点。你可以配置一些豁免规则，使得服主能封禁管理员、管理员能封禁协管，但是协管不能封禁管理员。

由于不存在统一的权限API，为了让该功能正常运作，LibertyBans需要你选择并安装一个支持程序：

1. LuckPerms的用户组权重
2. Vault权限

注意：
* 该功能阻止低级管理员处罚高级管理员的拒绝消息可以在messages.yml文件中配置。
* 针对IP地址的处罚不考虑豁免机制。豁免功能适合与复合处罚结合对玩家使用。
* 在处罚用户后为该用户赋予豁免权，并不能自动撤销现有的处罚。

### 基于LuckPerms用户组权重的豁免 [exemption-luckperms]

此扩展只能和LuckPerms共同使用，因为它利用了LuckPerms的用户组权重功能。

配置很简单。只需确保为用户组设置权重。高级的管理员用户组应当具有更高的权重。

管理员可以处罚用户组权重比他自己低的玩家。注意LibertyBans会考虑每名玩家的所有权限组，来确定该用户的最高用户组权重。

### 基于Vault权限的豁免 [exemption-vault]

此扩展根据带等级的权限提供豁免功能。这需要一个与Vault兼容的权限插件，且只支持Spigot或Paper服务器。

扩展通过定义豁免等级来运作。豁免等级越高，管理员权限也越高。豁免等级低的管理员无法处罚豁免等级高的管理员。

配置：
1. 授予权限`libertybans.<类型>.exempt.level.<豁免等级>`。
2. 将`max-level-to-scan-for`配置设置为你授予过的最高豁免等级。
3. 调整`permission-check-thread-context`配置的值来适配你的权限管理插件。

## Layouts [layouts]

The layouts addon provides the `/libertybans punish` command. It is a straightforward yet powerful means of defining punishment templates, ladders, tracks -- however you want to call them.

After a punishment is created via a layout track, it is treated like any other punishment. However, of course, new punishments created using the same track will apply a configured ladder to calculate punishment details.

### Configuration

The configuration works by defining a ladder for each layout track. Each entry on the ladder specifies the punishment to be applied when a player reaches that many (or more) punishments.

### Permission

Permissions to use layouts are similar for permissions to create punishments normally. However, permissions are specific to each layout. Replace `<track>` with the name of the layout track you want to grant permission for.

* `libertybans.addon.layout.use.<track>.target.uuid` - punish players
* `libertybans.addon.layout.use.<track>.target.ip` - punish IP addresses
* `libertybans.addon.layout.use.<track>.target.both` - punish player and IP address in the same punishment
* `libertybans.addon.layout.use.<track>.silent` - use the silent feature

Please note that the notification permissions remain tied to the punishment type. In other words, the permissions `libertybans.<type>.<do|undo>.<notify|notifysilent>` remain the same; there are no notification permissions specifically for layouts.

### Interaction with Exemption Permissions

If you are using the Vault permissions exemption addon, then the `libertybans.layout.exempt.level.<level>` permission defines exemption levels. (The typical permission cannot be used because exemption is checked before the punishment is executed).

## Other

### Shortcut Reasons [shortcut-reasons]

Allows substituting faster shortcuts for commonly-used punishment reasons. For example, `/ban A248 30d #hacking` becomes `/ban A248 30d You are banned for hacking`.

Configuration is straight-forward otherwise. If a staff member specifies an invalid shortcut, the command is denied to prevent mistakes. Shortcuts are case-sensitive.

### Warn Actions [warn-actions]

Allows executing actions, such as executing commands or inflicting additional punishments, when a certain amount of warns is reached.

This addon is relatively easy to use and configure.
