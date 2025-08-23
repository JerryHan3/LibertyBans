本页面是一个在LibertyBans，AdvancedBan，BanManager，和LiteBans之间进行对比的速查表格。

**特别注意：*本页面上的图标不能展示全貌！*** 如果您想要了解细节，请阅读详细的解释和比较文本。您可以在侧边栏找到它们。对于这里所示的每一个插件，都有一份与LibertyBans的详细对比文档。

## 总表

<!-- Platform logos -->

[Bukkit]:https://media.forgecdn.net/avatars/97/684/636293448268093543.png
[Sponge]:https://www.spongepowered.org/favicon.ico

<!-- License logos -->

[AGPL]:https://www.gnu.org/graphics/agplv3-155x51.png
[GPL]:https://www.gnu.org/graphics/gplv3-127x51.png
[CC-BY-NC]:http://mirrors.creativecommons.org/presskit/buttons/88x31/png/by-nc.png

| 插件      | 支持平台                                                                                                                                                                                                                                                                                                                                                      | Java版本要求 | 免费 | 开源               | 支持数据库                        | 线程安全设计 | 稳定的API | 支持Geyser | 支持多实例 | 使用连接池 | 豁免功能 | 服务器范围功能 | 预设/模板功能 | 使用UUID | 数据库完整性 | 可切换存储方式 | 支持的导入源                                                                                                                                        |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|---------------|----------------------------|--------------------------------------------|--------------------|------------|----------------|------------------------|-----------------|-----------|---------------|---------------------|------------|------------------|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| LibertyBans | ![Bukkit]Bukkit<br/> <img src="https://avatars.githubusercontent.com/u/1007849?v=4" width=16>Bungee<br/> <img src="https://www.spongepowered.org/assets/img/icons/spongie-mark.svg" width=16>Sponge <img src="https://raw.githubusercontent.com/PaperMC/velocitypowered.com/5878ae0941e3adff3a238fe9020250c5f01c2899/src/assets/img/velocity-blue.png" width=16>Velocity | 17+       | ✔️            | ✔️ ![AGPL]                 | HSQLDB (本地), MariaDB, MySQL, PostgreSQL | ✔️                 | ✔️         | ✔️             | ✔️                     | ✔️              | ✔️        | ✔️            | ✔️                  | ✔️         | ✔️               | ✔️                      | AdvancedBan<br/>BanManager<br/>LiteBans<br/>原版                                                                                                |
| AdvancedBan | ![Bukkit]Bukkit<br/> <img src="https://avatars.githubusercontent.com/u/1007849?v=4" width=16>Bungee                                                                                                                                                                                                                                                                      | 8+        | ✔️            | ✔️ ![GPL]                  | HSQLDB (本地), MariaDB, MySQL             | ❌️                 | ❌️         | ❓              | ❌️                     | ❌️              | ✔️        | ❌️            | ✔️                  | ➖️         | ❌️               | ❌️                      |                                                                                                                                                    |
| BanManager  | ![Bukkit]Bukkit<br/> <img src="https://avatars.githubusercontent.com/u/1007849?v=4" width=16>Bungee<br/> <img src="https://www.spongepowered.org/assets/img/icons/spongie-mark.svg" width=16>Sponge                                                                                                                                                                      | 8+        | ✔️            | ➖️️ ![CC-BY-NC]            | H2 (本地), MariaDB, MySQL                 | ❌️️                | ❌️         | ➖️️            | ✔️                     | ✔️              | ❌️        | ➖️            | ➖️                  | ✔️         | ✔️               | ➖️                      | AdvancedBan<br/>原版                                                                                                                            |
| LiteBans    | ![Bukkit]Bukkit<br/> <img src="https://avatars.githubusercontent.com/u/1007849?v=4" width=16>Bungee<br/> <img src="https://raw.githubusercontent.com/PaperMC/velocitypowered.com/5878ae0941e3adff3a238fe9020250c5f01c2899/src/assets/img/velocity-blue.png" width=16>Velocity                                                                                            | 8+        | ❌️            | ❌️ 闭源、代码混淆 | H2 (本地), MariaDB, MySQL, PostgreSQL     | ❓                  | ➖️         | ➖️️            | ✔️                     | ❓               | ➖️        | ➖️            | ✔️                  | ✔️         | ❌️               | ✔️                      | AdvancedBan<br/>BanManager<br/>LibertyBans➖️<br/>原版<br/>*+4 弃用的来源*<img src="https://clipart-library.com/data_images/508362.png" width=20> |
| 原版     | ![Bukkit]Bukkit<br/> <img src="https://www.spongepowered.org/assets/img/icons/spongie-mark.svg" width=16>Sponge                                                                                                                                                                                                                                                          | NA        | ✔️            | ❌️ 闭源             | 纯文本文件                                   | ✔️                 | ✔️         | ✔️             | ❌️                     | NA              | ❌️        | ❌️            | ❌️️                 | ✔️         | ❌️               | NA                      |                                                                                                                                                    |

图例：

✔️ – 是

➖️ – 部分

❌️ – 否

❓ - 未知（插件闭源、或功能尚未测试）

NA - 不适用

### 为什么LibertyBans的所有单元格都打了勾？

过去不是这样。这个表格是在LibertyBans还没有多实例支持、豁免功能、服务器范围配置、模板预设、或切换存储后端等功能的时候创建的。在这些功能尚不存在的时候，所有的功能都被列在了表格里面，但它们还没有被实现，也没人提出相关请求——也就是还没计划加入这些功能！那时，LibertyBans还有很多❌或➖️的标记。

时过境迁，这些功能陆续得到需求并被实现，因此LibertyBans现在满足这些类别的要求，并得到了✔️标记。同类插件里还有很多LibertyBans里面不存在的功能，但是就处罚玩家这个目的而言，它们的功能不算很重要或者很核心，因此没有在表格上出现。

我们是如何知道表格中列出的功能对于处罚插件是核心且重要的？在大多数情况下，我们会*预测*哪些功能最重要，并把它们列入表格中。这些预测最后被证实是准确的，因为表格中的这些类别也是功能请求中热度最高的几项。

## 类别

由于有些类别的含义不太明确，它们需要进一步的解释。以下是详细描述。

有些类别在这里描述起来太过复杂。您需要去读一下具体的插件对插件的对比页面来了解这些类别的细节。您可以在侧边栏里面找到这些页面。每一个插件都有一份与LibertyBans的详尽对比说明。

### 支持平台

即插件的稳定发布版所支持的软件平台。

### Java版本要求

即软件运行所要求的最低Java版本。

### 开源

即插件是否以自由软件许可证发布。有以下两点要求：
1. 源代码自由：软件公开了源代码
2. 使用自由：用户可以将软件用于任何目的

BanManager的许可证禁止将其用于商业用途。因此将其用于赚钱是**非法**的。尽管如此，它的源代码仍然时公开的，因此他得到了“部分”的标记。

LiteBans的代码经过了混淆，这意味着它的jar文件被刻意地进行了混淆处理，防止任何人研究其运作方式、调试问题、或进行任何修改。

免责声明：本页面不构成法律建议，其作者也不是律师。

### 线程安全设计

如果插件做不到线程安全，它的行为就会不稳定、很容易出现问题。不过，有些不稳定的行为只会在罕见的意外情况中出现，这使得开发者很难调试、分析这些问题。

请查阅详细的插件对比页面了解详情。

### 稳定的API

即插件的API是否遵循语义化版本控制，因此其他插件是否可以稳定地依赖它的API。

请参阅[semver.org](https://semver.org/)和详细的插件对比页面。

LiteBans的“部分”标记：LiteBans遵循语义化版本控制中对“主版本号”仅限于破坏性修改的要求，但是并没有遵循对新API的语义化版本要求，这理应在次版本号中予以指出。

### Geyser支持

即插件是否与Geyser、Floodgate兼容。这是通过修改用户名来使基岩版玩家得以进入服务器或跨服端的插件。

LiteBans的*部分*标记：LiteBans宣称与Geyser兼容，但根据其文档所述，默认的句点（.）字符是唯一支持的基岩版用户名前缀。

### Multi-Instance Support

This feature allows synchronizing punishments across multiple instances of the given plugin. It is relevant for proxies.

This is commonly used for multi-proxy setups, but can also be used for installing the plugin on the backend servers rather than the proxy.

### Connection Pool

Includes whether the plugin has a connection pool *and* takes advantage of it.

AdvancedBan has a connection pool, but in practice, can only use 1 connection at a time, which is effectively the same as not using a connection pool.

### Exemption

Whether the plugin can prevent lower-ranked staff from banning higher-ups through a system of exemption levels.

BanManager's *no* ranking: While BanManager has a basic exemption feature without levels, it requires every exempted player to be written out in the BanManager configuration. This is far too inconvenient in many cases, since it requires reconfiguring and reloading BanManager every time staff are promoted.

LiteBans' *partial* ranking: The plugin does not support arbitrary levels of exemption.

### Server Scopes

This feature is relevant for proxies. Whether the plugin has the ability to define "scopes" and create punishments applying to certain scopes. This allows server administrators to create punishments applying to a specific backend server or a group of backend servers.

BanManager's and LiteBan's *partial* ranking: BanManager has the ability to create a "local" punishment, meaning it applies to one backend server. However, it does not have the ability to define punishments applying to a group of backend servers; further, local punishments cannot be created from separate servers. LiteBans has server scopes, but similarly, it cannot create scopes applying to a group of servers.

### Layouts / Templates

Whether the plugin can automatically fill in details such as the reason and time, including based on the past history of the punished player.

BanManager's *partial* ranking: Reason shortcuts are provided; however, automatic time calculation based on past history is not implemented.

### Uses UUIDs

Whether the plugin stores UUIDs instead of player names, for both the targets of punishments and operators of punishments. Player names can change, so they cannot be relied upon.

AdvancedBan's *partial* ranking: AdvancedBan uses UUIDs for the targets of punishments. However, it uses player names for operators.

### Schema Integrity

Whether the data types defined by the plugin's database schema have appropriate constraints and are of the correct type.

* When a database schema has integrity, a bug in the plugin will *not* corrupt user data.
* Otherwise, bugs in the plugin may corrupt user data.

Data corruption, if it occurs, is not easy to recover from and may require manually interfacing with the database.

### Switch Storage Backends

Whether the user can switch between the supported database backends. This feature is also known as "self-importing."

BanManager's *partial* ranking: BanManager only supports converting from H2 to MySQL/MariaDB, but it is not possible to switch back to H2.

### Import From

The other punishment suites this plugin can import from.

LiteBans' *partial* ranking with respect to LibertyBans: LiteBans does not import server scopes, although scopes are a common feature between them.

Moreover, LiteBans can import from 4 abandoned plugins: BanHammer, BungeeAdminTools, MaxBans, and UltraBans. These plugins have received no codebase updates for at least 3 years.

--------------------------------------------------------------------------

As a closing note, this information is kept up-to-date within a reasonable timeframe. We welcome PRs from those affiliated with other plugins to update this information when necessary.
