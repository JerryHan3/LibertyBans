
LibertyBans以扩展程序的形式提供了一些额外功能。

安装扩展不会造成额外的性能开销：它们会直接注入LibertyBans的核心，而无需经过任何中间层。以扩展的形式实现功能是保持插件可持续开发的一种设计考量。

## s安装扩展

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

## Exemption

Exemption functionality allows you to protect certain players from punishment. For example, you may want to prevent moderators from banning administrators, and you never want the owner to be banned.

LibertyBans allows you to achieve this. You can configure exemption so that owners can ban admins, and admins can ban moderators, but moderators cannot ban admins.

Because there is no unified permissions API, LibertyBans requires you to choose and install an exemption backend for this feature to operate:

1. LuckPerms group weights
2. Vault permissions

Notes:
* The denial message when a staff member tries to punish a superior officer is configurable in the messages.yml file.
* IP-based punishments do not consider exemption. The exemption feature works best with user and composite punishments.
* Granting exemption to a user after the fact will not automatically undo existing punishments.

### Exemption with LuckPerms group weights [exemption-luckperms]

This addon works only with LuckPerms, since it leverages LuckPerms' group weights feature.

Configuration is simple. Make sure to configure LuckPerms' group weights. Higher staff ranks should have bigger weights.

An operator can punish a player if the target player has a lower group weight than the operator. Note that LibertyBans considers every group for each user to determine the user's highest group weight.

### Exemption with Vault permissions [exemption-vault]

This addon provides exemption functionality using tiered permissions. It requires a Vault-compatible permissions plugin and only supports Spigot/Paper servers.

The addon operates by defining exemption levels. The higher the exemption level, the more privileged the staff member. Staff members with a lower exemption level cannot punish staff members with a higher level.

Configuration:
1. Grant the permission `libertybans.<type>.exempt.level.<level>` . 
2. Set the `max-level-to-scan-for` to the value of the highest exemption level you granted.
3. Change the `permission-check-thread-context` value to suit your permissions plugin.

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
