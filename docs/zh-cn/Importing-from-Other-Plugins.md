LibertyBans支持从以下来源导入数据：

* AdvancedBan
* BanManager
* LiteBans
* 原版服务器封禁 (包括 Essentials)
  * 从原版服务器导入封禁数据需要您在导入过程中在Bukkit服务器上运行LibertyBans。导入完成之后，您就可以将LibertyBans移动到其他受支持的平台。
* LibertyBans自身，旨在进行存储后端转换。请查阅[自我导入](Self-Importing)页面了解更多信息。

如果您没有看到您使用的插件列在上面，请创建[新的反馈](https://github.com/A248/LibertyBans/issues)并描述您需要的功能。

# 导入步骤

1. 备份您的数据。备份数据永远是一个好的行为。如果您想要有额外的保障，请确保您还能恢复您的备份数据。
2. 调整`import.yml`的配置。
3. 运行导入命令 - `/libertybans import <source>`。

# 注意事项

导入操作并非完全对等的过程，因为不同插件使用了不同的存储方式。

## AdvancedBan和原版的UUID支持

| 导入来源        | UUID支持（目标） | UUID支持（操作者） |
|---------------|----------------|-----------------|
| AdvancedBan   | ✔️            | ❌              |
| BanManager    | ✔️            | ✔️              |
| LiteBans      | ✔️            | ✔️              |
| 原版           | ❌            | ❌              |



AdvancedBans和原版会在LibertyBans需要UUID的一些地方使用名称。LibertyBans在所有地方都使用UUID识别，所以在以上情况下LibertyBans会进行UUID查询。

UUID查询的执行方式取决于`config.yml`中的`uuid-resolution`和`server-type`配置。

* 如果您运行的是一个正常的正版登录服务器，您需要添加额外的API解析网站。否则，您的服务器就会因执行过多UUID查询而触发Mojang的速率限制：
```
player-uuid-resolution:
  server-type: 'ONLINE'
  web-api-resolvers:
    - 'ASHCON' // 示例 - 先加上这个
    - 'MOJANG' 
```

* 如果您运行的是一个离线（盗版）服务器，并且使用的是`CRACKED`UUID选项 - 即所有的玩家都使用盗版UUID - 您无需进行任何操作。LibertyBans会假设所有用户都是盗版用户，并自动计算他们的盗版UUID。

* 如果您运行的是一个离线服务器，并且使用的是`MIXED`UUID选项，这种情况下部分用户使用盗版UUID，部分用户使用正版UUID。此时LibertyBans无法进行任何UUID查询，有一些处罚记录会因为LibertyBans无法决定UUID而被跳过。
  * You can avoid losing punishments if all the users join the server first, or have joined the server since LibertyBans was installed. If the players have joined the server before, LibertyBans will remember their name and UUID, and so when the import occurs, LibertyBans will know the UUID of these players.

## LiteBans – Using  H2

If you used LiteBans with MariaDB, MySQL, or PostgreSQL, no additional setup is required. LibertyBans includes these drivers.

If you used LiteBans with H2, you will need to download and install the driver first:

1. Download the H2 driver jar:
  * [Direct download link](https://repo1.maven.org/maven2/com/h2database/h2/1.4.199/h2-1.4.199.jar)
  * [Maven Central link](https://mvnrepository.com/artifact/com.h2database/h2/1.4.199)
2. Find the `LibertyBans/internal/attachments` directory. Upload the driver jar here.
3. Restart the server.
4. Run the import process as you normally would.

For help, join the discord for support.
