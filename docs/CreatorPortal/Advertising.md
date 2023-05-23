# 接入游戏广告

::: tip 阅读本文大概需要20分钟

本文将帮助您快速了解游戏如何接入广告、广告规则及查看广告数据。

::: 

## 广告接入

### 广告代码编写

在需要接入广告的位置粘贴以下代码（参考[广告相关API](https://api-docs.ark.online/classes/Service.AdsService.html)），并在相应位置填写广告播放逻辑即可。

::: danger 使用前获取广告激活状态，如果广告未激活则隐藏广告相关功能

const isActive=AdsService.getInstance.isActive(AdsType.Reward)

:::

- 播放广告

``` TypeScript
//这里使用激励广告举例，全屏广告同理
AdsService.getInstance().showAd(AdsType.Reward, (isSuccess:boolean)=>{
    if(isSuccess){
        //广告播放完成回调，给奖励等在此进行
    } else {
        //广告加载或者播放失败，在此处理
        //实际上这里最大可能是233版本过低不支持广告
    }
});
```

- 广告Ready状态

广告直接调用showAd即可正常播放，如果有特殊业务需求需要判定广告是否准备好来展示某些游戏内功能，可以调用以下方法。

``` TypeScript
//广告是否准备好
AdsService.getInstance().isReady(AdsType.Reward, (isReady:boolean)=>{
    if(isReady){
        //广告准备好
    } else {
        //广告还未准备好
    }
});
```

- 广告类型

``` TypeScript
//广告类型
export enum AdsType {
    Reward = "reward",
        //激励
    Interstitial = "interstitial",
        //全屏
}
```

### 广告位关联

在将游戏发布或更新后，可在【创作者中心】-【游戏服务】-【[广告接入](https://portal.ark.online/#/admin/advertising-access)】点击游戏关联广告位。

![img](https://arkimg.ark.online/1684028057037-67.webp)

### 测试广告播放

通过[二维码](https://docs.ark.online/CreatorPortal/Advertising.html#获取游戏二维码)可拉起游戏并播放广告，根据游戏设定，触发广告播放，确保广告能够正常播放。

::: danger 注意

游戏正式发布前，请您先仔细阅读广告规则，广告不规范审核人员会驳回申请。

:::

## **广告合作规则**

### **接入要求**

口袋方舟致力于为创作者（以下或称“您”）提供一个优质的创作平台，为创作者及用户提供精彩体验，让平台健康、可持续发展。创作者需保证遵守适用法律、法规的规定，并遵守下列规范：

**1.创作者需保证创作内容、广告的展示内容合法合规，不得包含非法、误导性内容，若受众涉及未成年人，应当保护未成年人身心健康，保障未成年人合法权益。**

**2.创作者需保证广告展示/点击/消费等的行为主体来自于真实用户，在合作过程中不得出现如下行为：**

2.1制造无效流量（如：自行访问、鼓励访问、程序访问等）。

2.2制造无效点击：

（1）自己点击：用户本人或者煽动他人进行反复手动点击；

（2）强制和鼓励用户点击：以任何资源交换为目引导用户点击；

（3）通过程序软件点击：通过作弊程序，自动点击来增加无效数据。

2.3违规嵌入：

（1）出现诱导、引导用户对任意广告进行点击字样；

（2）广告遮盖媒体操作元素，影响用户正常操作；

（3）同一媒体界面嵌入多条广告，遮盖媒体界面，严重影响用户正常观看。

2.4其他以任何不正当方式制造虚假或无效流量、点击量、下载量等，或违规嵌入等任何行为。

**3.您应遵守本须知，否则，口袋方舟有权随时单方限制、中止或终止向您提供服务，包括但不限于采取通知整改、删除违规内容、冻结创作者帐号、暂停收益分成、扣除部分或全部收益分成等措施，并有权追究您的相关责任。**

4.本须知是《口袋方舟创作者协议》等平台相关规则等的补充协议，是其不可分割的组成部分，与其构成统一整体。本须知与上述内容存在冲突的，以本须知为准。

::: danger 注意

口袋方舟有权不定期制定和调整相应的创作者管理及处罚规则，相关处罚规则作为口袋方舟规则不可分割的组成部分，与其构成统一整体。

:::

### **广告触发要求**

1、应用内广告不得影响用户的正常操作体验；

2、禁止在应用的闪屏页、首页、退出页面弹出广告；

3、禁止在游戏操作进行中弹出广告，流程结束才能弹出（如角色死亡、关卡通过等）；

4、禁止遮挡、扭曲、模糊广告图片和内容，不能存在广告内容展示变形的情况；

5、应用内广告不得含有欺诈内容；

6、应用广告不得包含不良或违法广告或信息（如色情、赌博、反动等）；

7、应用广告不能有捆绑行为（如广告内默认勾选其他应用，造成用户下载）；

8、应用不能包含空白广告位或者招商广告位；

9、应用内广告需带有关闭功能，且应用关闭后，应用内广告也需同时关闭；

10、广告展示时间必须超过1s，否则作为无效广告展示；

11、禁止在同一触发点同时存在不同类型的广告；

12、禁止误触广告的场景设置，包括但不限于：

① 恶意诱导点击的虚假按钮或功能；
② 广告部分遮挡游戏功能性按键引导误触；
③ 设计需要连续点击的游戏按钮，在点击过程中突然出现广告；
④ 广告关闭按钮与游戏功能按键过近或重叠；
⑤ 非视频类广告不能用作激励场景（如：“看广告复活”“看广告获得奖励”“看广告签到”“看广告抽奖”“看广告开宝箱”“看广告减免”）。

### **广告实施规范**

- **激励视频广告**

展示形式：视频广告是长约15~30秒，广告观看完成后自动跳转到APP下载界面；

常见展示场景：

1. 通关：观看视频解锁新关卡；
2. 复活：观看视频复活；
3. 获取积分/道具/虚拟货币/皮肤/新角色/装备/额外空间等；
4. 获取游戏机会：提示/抽奖/游戏加速/增加游戏时长/收益翻倍等。

展示规则：

1. 激励视频广告按钮需增加观看提示，例观看广告可获取抽奖机会，应在按钮上注明“看广告抽奖”或在“广告按钮上增加视频小图标”；
2. 用户未看完激励视频广告，不应该发放奖励；
3. 禁止激励视频广告设计包括但不限于：

- 开始游戏按钮默认播放广告，并没有取消广告的功能；
- 开始游戏按钮默认播放广告，并默认勾选；
- 开始游戏按钮默认播放广告，没有默认勾选，但是关闭选项很小，字体很浅或过一部分时间之后再出现；
- 用户进入激励场景，跳过/关闭按钮不能与广告内容或其他位置重合。

- **全屏视频广告**

展示形式：视频广告是长约15~30秒，观看5秒后可点击关闭，广告观看完成后自动跳转到APP下载界面；

常见展示场景：游戏/应用的暂停/通关/死亡结算等界面；

展示规则：

1. 禁止在开始操作进程中弹出全屏视频广告；
2. 禁止在弹出的广告上增加诱导按钮或增加虚假关闭按钮引起用户误点；
3. 禁止将全屏视频广告用于用户激励行为；
4. 禁止在游戏开始60秒内弹出全屏视频广告；
5. 全屏视频广告的单用户展示间隔不能小于60s。

## **广告数据**

![img](https://arkimg.ark.online/1684028057037-68.webp)

当您的游戏上线并接入广告后，昨日广告收益会展示在【[我的游戏](https://portal.ark.online/#/admin/game-list)】（红色相比前日上涨、绿色相比前日下跌），【点击数据】可快速进入当前游戏详细广告看板，一般会在下午计算完前一天的广告收益。

![img](https://arkimg.ark.online/1684028057037-69.webp)

::: danger 广告计算公式

广告总收益 = 广告播放次数 * ecpm / 1000 = DAU * 人均广告次数 * ecpm / 1000。

:::

> 由上述公式可见，提高广告收益的核心是要么提高游戏整体DAU、要么提高人均广告次数；

![img](https://arkimg.ark.online/1684028057038-70.webp)

- **预估总收益**：预估当天能得到的广告收入，注意此处为分成后的广告收益；
- **ECPM**：有效的1000次广告展现价格（Effective Cost Per Mile）一般受广告整个市场影响；
- **广告ARPU**：当前游戏的总广告收入/当前游戏的总日活DAU，是游戏商业化收入的重要指标；
- **人均广告次数**：当前游戏的总广告次数/当前游戏的总日活DAU，另一个影响游戏收入的重要指标，可通过提高游戏平均时长、丰富广告场景来提升游戏整体人均广告次数；