#信鸽基础介绍
![](/assets/jichu01.png)

##平台简介
<hr>

信鸽（XG Push）是一款专业的移动App推送平台，支持百亿级的通知/消息推送，秒级触达移动用户，现已全面支持Android和iOS两大主流平台。

开发者可以方便地通过嵌入SDK，通过API调用或者Web端可视化操作，实现对特定用户推送，大幅提升用户活跃度，有效唤醒沉睡用户，并实时查看推送效果。

##推送场景定义

### 推送通知
<hr>

在信鸽产品中，通知定义为Android和iOS开发者指南中的Notification。服务器定向将信息实时送达手机，通过建立一条手机与服务器的连接链路，当有消息需要发送到手机时，通过此链路发送即可。

通过推送一条用户可见的信息，引导用户进行有目的性的操作。通常用于产品信息知会、新闻推送和个性化消息等场景。

![](/assets/jichu02.png)

###本地通知
<hr>

本地通知定义为Android开发者指南中的Local Notification。

应用通过自定义的日期、时间和消息内容，无需通过服务器即可向用户推送一条可见的信息。通常用于应用的某些本地定时提醒场景，游戏应用中建筑物升级结束的提醒，以及一些有明确结束时间的场景等。

![](/assets/jichu03.png)

更多请参考XGPushManager提供信鸽服务的对外API列表

### 应用内消息
<hr>

在信鸽产品中，我们支持通过推送可执行代码指令，让应用在后台进行一系列操作行为，通过此功能，可以用最小成本实现对应用的远程操控，推送的应用内消息内容由各个应用开发者自定义。消息不弹出通知栏。

应用内消息可以支持的场景非常广泛，可以任由开发人员扩展。

例如给部分标签用户进行消息命令推送，让应用在WIFI情况下自动下载安装包并静默升级至最新；快速增量更新应用，或让应用根据自身情况下载并静默增量更新，对于不需要更新的用户不造成干扰。

另外，应用内消息既可以展示在通知栏里，也可以直接做成app的消息中心，所以自由度比推送通知栏消息高出百倍。

![](/assets/jichu04.png)![](/assets/jichu05.png)

### 标签
<hr>

在信鸽产品中，标签通常是指给某个一群用户打上标签，例如在北京的喜爱美食的使用iOS的用户；超过30天未启动应用的沉睡用户；高消费潜力用户；团队测试用户等。

一个应用最多有10000个 标签（tag）， 每个token在一个应用下最多100个 标签（tag）， 标签（tag）中不准包含空格。

地理标签、应用版本、流失用户这三个标签，是信鸽默认提供的，可以直接使用。
![](/assets/jichu06.png)

### 账号
<hr>

在信鸽产品中，别名/帐号通常是指给某特定用户推送消息。别名/帐号可以是终端在注册时上报的QQ号、openid、邮箱帐号、手机号等。

这里强调，若希望推送帐号，必须首先将账号与token进行绑定，否则将无法推送成功。绑定方式见Android、iOS接入指南——根据帐号推送。

目前一个帐号下，最多绑定15个设备token，超出后会随机顶掉前面绑定的一个token。
![](/assets/jichu07.png)

##常见问题
<hr>

**Q1:iOS SDK中有没有使用热更新或者私有接口？**

A:信鸽SDK没有使用过热更新或私有接口，不会影响苹果审核。

**Q2:推送数量/推送频率限制？**

A:推送数量无限制。推送频率上，仅全量广播限频为每3秒一次，其他推送行为不限频。

**Q3:对单个设备，保存多少条离线信息？保存时间？**

A:离线消息Android最多保存5条，iOS最多保存1条；保存时间最多72小时。

**Q4:标签方面限制？**

A:单个设备最多设置100个标签，单个app全局最多可以有10000个不同的标签。

**Q5:信鸽与腾讯开放平台的APPID数据是否相通？**

A:当你在开放平台注册应用并使用信鸽后，应用的信息会自动从开放平台同步至信鸽平台，单独使用信鸽时不用重新接入应用。但是，在信鸽接入的应用不会同步至开放平台。

**Q6:当第一次注册成功后，没有反注册，以后使用还需要注册吗？**

A:不需要，只要没反注册，就不需要再次注册

**Q7:应用关闭或结束进程后，还能收到推送消息吗？**

A:信鸽推送主要依赖信鸽的service进行消息的收发，杀死进程之后信鸽service也被杀死，只能等待service被拉活或重启app才可以收到推送。若手机中有其他接入信鸽的app被打开，则可以利用其他app的service接收消息，但共享service通道也受手机ROM限制，无法保证百分之百的成功率。

**Q8:设备注册为什么收不到回调信息？**

A:注册操作中，后台只可能有三种出错行为：

(1)不响应；

(2)返回错误格式的数据包；

(3)返回错误码。这三种行为终端应该都可以检测到并给出回调。

**Q9:为什么我推送成功了，有了抵达量，点击量却等于0？**

iOS点击量统计需要调用特殊代码，具体请参考iOS开发文档。

**Q10:为什么会出现推送通知时，只有声音却没有文字信息的情况？**

A:该问题与系统有很大关系，需要拿设备的logcat来进行特定分析。

**Q11:token与Account区别？**

A:token是一台设备（device）的标识，账号是一个用户（users）的标识。一个token只能绑定一个账号，多次绑定时，以最后一次为准。

**Q12:账号在设备A上登录过，又在设备B上登录？给这个账号发信息会怎么样？**

A:只要是没有注销，则两台设备都会收到

**Q13:标签与账号的区别？**

A:标签是用于标识一个token或用户的一些属性，如广东省、男性、游戏玩家等。帐号是用户的账号，请勿用标签作为别名使用。

**Q14:在应用列表中看到“覆盖设备数”，具体指的是什么？**

A:是指该应用下处于注册状态的设备数/终端数，同时也是该应用在推送时可以覆盖到的最大设备数。终端若调用了unregister的接口，覆盖设备数会减少。

**Q15:为什么在web端推送出现服务器繁忙？**

A: 请先检查token以及所选推送环境是否正确，然后检查证书是否正确提交，若还出现相同错误可重新制作一份不带密码的证书提交再试。

**Q16:推送过程中，非定时推送（立即推送）能否撤销？**

A:不能，只有返回push_id的任务才可以做撤销操作。

**Q17:推送后查看推送列表，已经推送完成了，状态却显示推送中，怎么办？**

A:刷新再试试。

**Q18:在推送时，如何向单个用户推送消息？**

A:请参考开发手册，有关于“推送消息给单个设备”和“推送消息给单个账户或别名”的使用指南。

**Q19:用户重连上线后收到多条push的顺序是怎样？**

A:按照消息ID递增。客户端也是按照此规则收取消息，因此，收消息的顺序就是发消息的顺序。

**Q20:我现在有安卓的用户和iOS的用户，那我php后台要写两个不同的接口分别推给安卓用户和ios用户吗？**

A:需要调用两次推送接口 也可以把两个封装为一个。

**Q21:如果定时push选择的是过去的时间，是不是不会push出去？**

A:不是，选择过去的时间系统则会立刻发送。

