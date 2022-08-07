![image](https://user-images.githubusercontent.com/37653613/183275817-0af95293-6466-4be3-9664-c4a6af1564bf.png)

Genshin Impact Helper

更新
原神签到小助手已更新至2.0.0，该更新为破坏性更新，请看完更新提示。
更新频道：https://t.me/genshinhelperupdates
备用群组：https://t.me/genshinhelper2

源码
https://github.com/y1ndan/genshinhelper2
https://gitlab.com/y1ndan/genshinhelper2
https://gitlab.com/y1ndan/genshin-checkin-helper

genshinhelper 从v2.0.0开始，分为genshinhelper2和genshin-checkin-helper两个项目，同时分离出onepush推送包。

genshinhelper2 - 签到相关的封装库，不能开箱即用。
genshin-checkin-helper - 签到主程序。
onepush - Push all in One. 一个简单易用的推送包。

之前终端运行 genshinhelper or python -m genshinhelper可以直接运行签到脚本，现在改为将论坛cookie转换为米游币cookie。

# 配置文件config.json变化：

## 新增变量

RANDOM_SLEEP_SECS_RANGE：随机延迟休眠秒数范围，单位：秒。设置成"0-0"为取消延迟。
CHECK_IN_TIME：每日签到时间。该时间和运行环境的时间有关，和时区无关。如果是docker，可以用TZ=Asia/Shanghai设置时区。
CHECK_RESIN_SECS：原神原粹树脂检测间隔时间，单位：秒。
COOKIE_RESIN_TIMER：需要开启原粹树脂检测账号的cookie。
SHOPTOKEN：微信积分商城的token，通过抓包获取。
ONEPUSH：推送配置。notifier为推送名字，params为所需参数。详见后文。

## 修改变量

COOKIE_WEIBO：国际版微博抓包后，请求地址里?后的全部参数。
例如：
https://api.weibo.cn/2/xxxxxx?aid=xxx&c=weicoabroad&from=123&gsid=_xxx&i=xxx&lang=zh_CN&s=xxx&ua=iPhone12%2C1_iOS14.0.1_Weibo_intl._4330_cell&v_p=59

COOKIE_WEIBO= aid=xxx&c=weicoabroad&from=123&gsid=_xxx&i=xxx&lang=zh_CN&s=xxx&ua=iPhone12%2C1_iOS14.0.1_Weibo_intl._4330_cell&v_p=59

## 移除变量

CRON_SIGNIN
MAX_SLEEP_SECS
RUN_ENV
BARK_KEY
BARK_SOUND
COOL_PUSH_SKEY
COOL_PUSH_MODE
CUSTOM_NOTIFIER
DD_BOT_TOKEN
DD_BOT_SECRET
DISCORD_WEBHOOK
IGOT_KEY
PUSH_PLUS_TOKEN
PUSH_PLUS_USER
SCKEY
SCTKEY
TG_BOT_API
TG_BOT_TOKEN
TG_USER_ID
WW_ID
WW_APP_SECRET
WW_APP_USERID
WW_APP_AGENTID
WW_BOT_KEY

Features

新增 原神原粹树脂溢出提醒
新增 原神微信积分商城签到
新增 社区任务签到支持崩坏：星穹铁道
新增 社区任务签到支持显示当前米游币
新增 hoyolab国际服支持显示角色服务器
新增 hoyolab国际服支持显示旅行者札记Traveler‘s Diary
Fixes

修复 微博超话检测失效
云原神签到也已支持，需要自己抓包填写CLOUD_GENSHIN变量。

注意：

下列参数如果required字段包含 'title' 或 'content'，ONEPUSH变量中都不需要设置。例如serverchan不需要设置 'title'。
custom方式暂时不支持推送签到结果。
OnePush配置讲解

在配置文件中，设置ONEPUSH变量开启推送
"ONEPUSH": {
"notifier": "",
"params": {

"markdown": false
}

如果使用环境变量，需要写成
ONEPUSH={"notifier":"","params":{"markdown":false}}
如果报错，可以添加单引号试试看
ONEPUSH='{"notifier":"","params":{"markdown":false}}'

ONEPUSH有两个字段
notifier: 推送名字
params: 推送参数

OnePush推送参数一览
推送名称 / notifier: bark
参数大全 / params:
{'required': ['key'], 'optional': ['title', 'content', 'sound', 'isarchive', 'icon', 'group', 'url', 'copy', 'autocopy']}

推送名称 / notifier: custom
参数大全 / params:
{'required': ['url'], 'optional': ['method', 'datatype', 'data']}

推送名称 / notifier: dingtalk
参数大全 / params:
{'required': ['token'], 'optional': ['title', 'content', 'secret', 'markdown']}

推送名称 / notifier: discord
参数大全 / params:
{'required': ['webhook'], 'optional': ['title', 'content', 'username', 'avatar_url', 'color']}

推送名称 / notifier: pushplus
参数大全 / params:
{'required': ['token', 'content'], 'optional': ['title', 'topic', 'markdown']}

推送名称 / notifier: qmsg
参数大全 / params:
{'required': ['key'], 'optional': ['title', 'content', 'mode', 'qq']}

推送名称 / notifier: serverchan
参数大全 / params:
{'required': ['sckey', 'title'], 'optional': ['content']}

推送名称 / notifier: serverchanturbo
参数大全 / params:
{'required': ['sctkey', 'title'], 'optional': ['content', 'channel', 'openid']}

推送名称 / notifier: telegram
参数大全 / params:
{'required': ['token', 'userid'], 'optional': ['title', 'content', 'api_url']}

推送名称 / notifier: wechatworkapp
参数大全 / params:
{'required': ['corpid', 'corpsecret', 'agentid'], 'optional': ['title', 'content', 'touser', 'markdown']}

推送名称 / notifier: wechatworkbot
参数大全 / params:
{'required': ['key'], 'optional': ['title', 'content', 'markdown']}

例子
telegram
ONEPUSH={"notifier":"telegram","params":{"markdown":false,"token":"xxxx","userid":"xxx"}}

discord
ONEPUSH={"notifier":"discord","params":{"markdown":true,"webhook":"https://discord.com/api/webhooks/xxxxxx"}}

docker 配置文件映射目录为：/etc/genshin:/app/genshincheckinhelper/config

时间匆忙，没细心排版，请见谅。如有疑问，可以在评论区留言或加入交流群。

关于回复后查看的问题，不需要注册账号，不需要审核，发完评论后刷新一下页面就可以了。

以下为 1.7.1 版本教程，请结合更新部分内容食用！！！
以下为 1.7.1 版本教程，请结合更新部分内容食用！！！
以下为 1.7.1 版本教程，请结合更新部分内容食用！！！

前言
原神是少有的游戏本体和签到福利分离的游戏，玩家为了签到还要额外下载米游社 App。

平心而论，目前的每日签到奖励真的不咋地，都知道是蚊子腿。事实上，你完全可以选择无视签到，不签也没啥大的损失；或者选择手动签到，但这样的话哪天忘记打卡了就很头疼。

为了原石、摩拉和紫色经验书等签到奖励，这个项目应运而生，可以实现自动每日签到。

简介
genshinhelper(原神签到小助手)，前身为 genshin-impact-helper，可以自动化为你获取原神每日福利



特性
支持订阅推送 可选多种订阅方式，每天将签到结果推送给用户
支持多个账号 不同账号的 Cookie 值之间用#分隔，如：cookie1#cookie2#cookie3
天空岛/世界树

米游社原神每日签到
米游社区任务
微博超话签到
原神超话功能 活动监测 + 领兑换码 + 多方推送
支持多个角色 支持绑定官服和B站服的米游社账号
虎扑原神签到 未实现
America/Europe/Asia/SAR

米游社国际版(HoYoLAB)原神每日签到
准备
获取 Cookies
在开始使用前，需要先获取相应配置，你可以在 配置章节找到本项目使用的所有环境变量。

各种订阅方式的 Token 或 Key 可以在对应网站的使用文档中找到获取方法，这里不再赘述；而目标网站的 Cookies 需要自己获取。

原神签到福利
米游社：https://bbs.mihoyo.com/ys/
Cookie 应包含account_id和cookie_token两个字段

崩坏3福利补给
同原神签到

米游社区任务

这部分问的小伙伴最多，但是不好明白讲出来，特地设置个隐藏，请见谅哈
米游社区任务即米游币签到，获取 Cookie 的方法和米游社一样，但注意米游币需要account_id、cookie_token和login_ticket三个字段。

account_id 和 cookie_token 参数到米游社获取
login_ticket 参数到个人中心获取
注意：推荐使用浏览器的无痕模式登录以上网站，如果你有多个账号，获取后不要退出上一个账号，而是直接新建一个无痕窗口登录第二个账号

获取的 Cookie 有 30 分钟有效期，所以要尽快执行下一步转换 Cookie 的操作：

转换 Cookie 有 2 种方法：

使用 genshinhelper 命令

pip install genshinhelper
python -m genshinhelper
然后填入 Cookie 进行转换

使用 1.7.1 版本云函数
新建一个 1.7.1 版本云函数，将 Cookie 填 入COOKIE_MIYOUBI 运行一次。如果报错：YOUR COOKIE_MIYOUBI: xxxxxx，那么这是正常的，其中的xxxxxx就是转换后的 Cookie
将转换后的 Cookie 填至最新版的COOKIE_MIYOUBI就能正常运行了。

米游社国际版
HoYoLab：https://webstatic-sea.mihoyo.com/ys/event/signin-sea/index.html?act_id=e202102251931481&lang=en-us
Cookie 应包含account_id和cookie_token两个字段

微博超话签到
特别地，微博参数需要在 微博国际版App 抓包取得。

在抓包结果请求头里提取出aid、s、gsid和from参数，自行组合成形如 ”aid=xxx; s=xxx; gsid=xxx; from=xxx“的形式。

如果是使用iOS设备，可参考这个视频：微博国际版iOS抓包教程

原神超话监测
新浪新手卡：https://ka.sina.com.cn/
Cookie 需要SUB和SUBP两个字段。

提示：获取的Cookie 应包含上述字段，否则视为获取失败。这时可尝试退出账号，打开无痕模式重新获取。
提示：Cookie 支持配置多个，不同账号的 Cookie 值之间用 #分隔，如：COOKIE_MIHOYOBBS="cookie1#cookie2#cookie3"。
鼠标按住并拖动以下图片或按钮到你的浏览器书签栏
打开目标网站
点击刚刚添加的书签
复制弹出的Cookies
Ganyu Cookies Getter

部署
项目支持 Docker、PyPI和云函数三种安装方式，请根据实际情况选择相应版本安装。

提示：如果选择 Docker或 PyPI安装方式，请确保已事先安装好了 Docker或 Python3环境
choose_platform
choose_platform

Docker
PyPI Package
云函数
使用以下命令拉取镜像：

docker pull yindan/genshinhelper
Bash 复制
这将拉取最新的 genshinhelper镜像。

你可以在Docker Hub上找到该仓库。

订阅
支持 Bark App 、
酷推、钉钉机器人、Discord、iGot聚合推送、pushplus、Server酱、Telegram robot、企业微信应用、企业微信机器人和自定义推送
单个或多个推送，通过配置环境变量或填写配置文件开启对应推送方式，变量名称列表详见下文 环境变量部分内容。

自定义推送
{
    "method":"post",
    "url":"",
    "data":{
  
    },
    "retcode_key":"",
    "retcode_value":200,
    "data_type":"data",
    "merge_title_and_desp":false,
    "set_data_title":"",
    "set_data_sub_title":"",
    "set_data_desp":""
}
JSON 复制
Custom notifier:
    method:                 Required, the request method. Default: post.
    url:                    Required, the full custom push link.
    data:                   Optional, the data to sent. default: {}, you can add additional parameters.
    retcode_key:            Required, the key of the status code returned by the response body.
    retcode_value:          Required, the value of the status code returned by the response body.
    data_type:              Optional, the way to send data, choose from params|json|data, default: data.
    merge_title_and_desp:   Optional, if or not the title (application name + running status) and the running result will be merged. Default: false.
    set_data_title:         Required, the key of the message title in the data of the push method.
    set_data_sub_title:     Optional, the key of the message body in the push data.
    set_data_desp:          Optional, the key of the message body in the push data.

自定义推送:
    method:                 必填,请求方式.默认: post.
    url:                    必填,完整的自定义推送链接.
    data:                   选填,发送的data.默认为空,可自行添加额外参数.
    retcode_key:            必填,响应体返回的状态码的key.
    retcode_value:          必填,响应体返回的状态码的value.
    data_type:              选填,发送data的方式,可选params|json|data,默认: data.
    merge_title_and_desp:   选填,是否将标题(应用名+运行状态)和运行结果合并.默认: false.
    set_data_title:         必填,推送方式data中消息标题的key.
    set_data_sub_title:     选填,推送方式data中消息正文的key.有的推送方式正文的key有次级结构,需配合set_data_title构造子级,与set_data_desp互斥.
                                例如: 企业微信中,set_data_title填text,set_data_sub_title填content.
    set_data_desp:          选填,推送方式data中消息正文的key.例如: server酱的为desp.
                                与set_data_sub_title互斥,两者都填则本项不生效.
例子：
写一个 ServerChan 的自定义推送。

查看文档得到 ServerChan 推送所需要的信息：
需要的 url形式为：https://sc.ftqq.com/{SCKEY}.send
发送的 data形式为：{'text': test','desp':desp}
消息发送成功响应体为：{'errno': 0, 'errmsg': 'OK'}

自定义推送配置如下：

{
    "method":"post",
    "url":"https://sc.ftqq.com/{直接填写你的SCKEY}.send",
    "data":{
  
    },
    "retcode_key":"errno",
    "retcode_value":0,
    "data_type":"data",
    "merge_title_and_desp":true,
    "set_data_title":"test",
    "set_data_sub_title":"",
    "set_data_desp":"desp"
}
JSON 复制
提示：若开启订阅推送，无论成功与否，都会收到推送通知。
配置
项目有两种使用自定义配置的方式：

环境变量
直接将你的配置写入环境变量。

下表包含了本项目所用到的全部环境变量

注意：有的变量（大部分是推送相关的变量）已经废弃了，请参考更新部分内容！

Variable Name	Required	Default	Description
LANGUAGE	❌	en	项目语言。目前支持中文(zh)和英文(en)。
MAX_SLEEP_SECS	❌	300	最大休眠秒数。自v1.5.0添加了运行前随机延迟，设置此参数可自定义延迟，秒数应该＞10
RUN_ENV	❌	prod	运行环境。设置为任意非默认值即可跳过随机延迟。
COOKIE_MIHOYOBBS	❌		Cookie from miHoYo bbs. https://bbs.mihoyo.com/ys/
COOKIE_BH3	❌		和 COOKIE_MIHOYOBBS 一样
COOKIE_MIYOUBI	❌		Cookie from miHoYo bbs. https://bbs.mihoyo.com/ys/
COOKIE_HOYOLAB	❌		Cookie from HoYoLAB community. https://webstatic-sea.mihoyo.com/ys/event/signin-sea/index.html?act_id=e202102251931481&lang=en-us
COOKIE_WEIBO	❌		Parameters from Sina Weibo intl. app. aid=xxx; gsid=xxx; s=xxx; from=xxx
COOKIE_KA	❌		Cookie from https://m.weibo.cn
BARK_KEY	❌		iOS Bark app's IP or device code. For example: https://api.day.app/xxxxxx
BARK_SOUND	❌	healthnotification	iOS Bark app's notification sound. Default: healthnotification
COOL_PUSH_SKEY	❌		SKEY for Cool Push. https://cp.xuthus.cc/
COOL_PUSH_MODE	❌	send	Push method for Cool Push. Choose from send(私聊),group(群组),wx(微信). Default: send
CRON_SIGNIN	❌	0 6 *	Docker custom runtime
CUSTOM_NOTIFIER	❌		Custom notifier configuration
DD_BOT_TOKEN	❌		钉钉机器人WebHook地址中access_token后的字段.
DD_BOT_SECRET	❌		钉钉加签密钥.在机器人安全设置页面,加签一栏下面显示的以SEC开头的字符串.
DISCORD_WEBHOOK	❌		Webhook of Discord.
IGOT_KEY	❌		KEY for iGot. For example: https://push.hellyw.com/xxxxxx
PUSH_PLUS_TOKEN	❌	一对一推送	pushplus 一对一推送或一对多推送的token.不配置push_plus_user则默认为一对一推送. https://www.pushplus.plus/doc/
PUSH_PLUS_USER	❌		pushplus 一对多推送的群组编码.在'一对多推送'->'您的群组'(如无则新建)->'群组编码'里查看,如果是创建群组人,也需点击'查看二维码'扫描绑定,否则不能接收群组消息.
SCKEY	❌		SCKEY for ServerChan. https://sc.ftqq.com/3.version/
SCTKEY	❌		SENDKEY for ServerChanTurbo. https://sct.ftqq.com/
TG_BOT_API	❌	api.telegram.org	Telegram robot api address. Default: api.telegram.org
TG_BOT_TOKEN	❌		Telegram robot token. Generated when requesting a bot from @botfather
TG_USER_ID	❌		User ID of the Telegram push target.
WW_ID	❌		企业微信的企业ID(corpid).在'管理后台'->'我的企业'->'企业信息'里查看. https://work.weixin.qq.com/api/doc/90000/90135/90236
WW_APP_SECRET	❌		企业微信应用的secret.在'管理后台'->'应用与小程序'->'应用'->'自建',点进某应用里查看.
WW_APP_USERID	❌	@all	企业微信应用推送对象的用户ID.在'管理后台'->' 通讯录',点进某用户的详情页里查看.默认: @all
WW_APP_AGENTID	❌		企业微信应用的agentid.在'管理后台'->'应用与小程序'->'应用',点进某应用里查看.
WW_BOT_KEY	❌		企业微信机器人WebHook地址中key后的字段. https://work.weixin.qq.com/api/doc/90000/90136/91770
配置文件
推荐将配置文件模板 config.example.json 拷贝并重命名为 config.json再填入你的配置；也可以直接使用 config.example.json 文件。

配置文件可以只留下需要的参数，把非必须的参数删除。

例如只配置原神签到福利和Discord推送，那么配置文件除了保持完整也可以写成：
‌

{
  "COOKIE_MIHOYOBBS": "",
  "DISCORD_WEBHOOK": ""
}
JSON 复制
致谢
感谢XiaoMiku01的 miyoubiAuto.
感谢所有为 y1ndan/genshin-impact-helper 项目贡献代码的大佬们以及使用过该项目的小可爱：
@PomeloWang
@Celeter
@Arondight
@chenkid999
@xe5700
@Renari
@journey-ad
@aflyhorse
@thesadru
@PeterPanZH
@cainiaowu
@alwaysmiddle
@qianxu2001


# genshinhelper

A Python library for miHoYo bbs and HoYoLAB Community.

## Installation

Via pip:

```
pip install genshinhelper
```

Or via source code:

```
git clone https://github.com/y1ndan/genshinhelper2.git
cd genshinhelper2
python setup.py install
```

## Basic Usage

```python
import genshinhelper as gh

cookie = 'account_id=16393939; cookie_token=jPjdK4yd7oeIifkdYhkFhkkjde00hdUgh'
g = gh.Genshin(cookie)
roles = g.roles_info
print(roles)
```

