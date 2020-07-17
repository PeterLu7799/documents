# Huajiao Superfast version development notes

## Steps to create the new target:

1. Create new Git branch from release of v7.2.5
2. Duplicate the "living" target as "livingSuperfast"
3. Changed bundle id to be "com.huajiao.lite"
4. Changed Podfile to add the support for new target
5. Removed the three extensions
6. Add SUPERFAST_VERSION in Preprocessor Macros of Build Settings


## Added two new notification targes

1. Duplicate the two notification extension targets from origins
2. Changed the Bundle IDs
3. Changed the Group IDs
4. Changed the entitlement files
5. Changed the Info plist file
6. Added the two extensions to livingSuperfast target 

## Code changes via SUPERFAST_VERSION macro

1. Removed the Live button in the tabbar
2. Removed My MV Video and Anchor related options in Mine page
3. Removed the Go Live guide
4. Removed the 5 options in Settings page
5. Replaced the app icon
6. Added APPNAME=huajiao_lite as common paramenter in service call
7. Changed the push devicetoken to report at "lite_pushid"
8. 3D Touch for Go Living is removed
9. Go Living from URL scheme is blocked and now showing an alertview
10. Web view's User Agent append string “huajiao_lite”
11. Changed Group IDs 
12. Changed Universal Link
13. Added common post parameter "open_appkey" for economic service calls
14. Aded "huajiao_lite" in User Agent
15. Changed Alipay app scheme


## Replacements of QiHu SDKs

* QIHUAI.framework (fabby，魔法背景) (Done)
* libqhface.a (face recognition) (Done)
* Gesture.framework (魔法手势) (Done)
* AIMakeUp360.framework (基础和高级美颜) (Done)
* libQHMakeup.a (微整形) (Warting for the lib)
* AIGreenScreen.framework (绿幕) (Done)


## Shrink package

### Code removal

1. Removed Go Live code files

	* HJSeedingViewController_v2 and all its categories
	* HJSeedEndView
	* HJSeedEndAchievementView
	* HJSeedEndHeadView
	* HJSeedEndImagesView
	* HJSeedEndBaseView
	
2. Removed My MV files:

	* HJMYMVViewController
	* HJMVPlayViewController
	* HJMVCuterViewController

### SDK removal 

1. BytedEffectsSDK (抖音美颜库)

## Replacement of the Third-party appid or appkey

1. Weixin appid and AppSecret 
2. QQ appid
3. Weibo appid
4. QDas appkey
5. QMapLocationGeocoder appkey
6. PEPLocationAndGeoManager
7. JVAuthConfig

## In-app Purchase Products

Name | Type | ID
---- | ---- | ----
1元包 | Consumable | fastpay.1.ios.lite.huajiao.com
6元包 | Consumable | fastpay.6.ios.lite.huajiao.com
42花椒豆 | Consumable | 6.ios.lite.huajiao.com
210花椒豆 | Consumable | 30.ios.lite.huajiao.com
686花椒豆 | Consumable | 98.ios.lite.huajiao.com
2086花椒豆 | Consumable | 298a.ios.lite.huajiao.com
4116花椒豆 | Consumable | 588.ios.lite.huajiao.com
11186花椒豆 (Removed) | Consumable | 1598.ios.lite.huajiao.com
6元礼物包 | Consumable | giftitem.6.ios.lite.huajiao.com
12元礼物包 | Consumable | giftitem.12.ios.lite.huajiao.com
18元礼物包 | Consumable | giftitem.18.ios.lite.huajiao.com
25元礼物包 | Consumable | giftitem.25.ios.lite.huajiao.com
68元礼物包 | Consumable | giftitem.68.ios.lite.huajiao.com
粉丝团订阅 | Non-Renewing Subscription | clubvip.1.ios.lite.huajiao.com
3个月粉丝团订阅 | Non-Renewing Subscription | clubvip.3.ios.lite.huajiao.com
6个月粉丝团订阅 | Non-Renewing Subscription | clubvip.6.ios.lite.huajiao.com
青铜贵族季卡(非自动续费型订阅) | Non-Renewing Subscription | noble.805.ios.lite.huajiao.com	
青铜贵族季卡续费(非自动续费型订阅) 	 | Non-Renewing Subscription | noble.805a.ios.lite.huajiao.com	
青铜贵族特权续费(非自动续费型订阅) 	 | Non-Renewing Subscription | noble.198a.ios.lite.huajiao.com	
青铜贵族特权首次开通(非自动续费型订阅)  | Non-Renewing Subscription | noble.298.ios.lite.huajiao.com	
骑士贵族季卡(非自动续费型订阅) 	 | Non-Renewing Subscription | noble.184.ios.lite.huajiao.com	
骑士贵族季卡续费(非自动续费型订阅) 	 | Non-Renewing Subscription | noble.184a.ios.lite.huajiao.com	
骑士贵族特权开通 			 | Non-Renewing Subscription | noble.68.ios.lite.huajiao.com
骑士贵族特权续费(非自动续费型订阅) 	 | Non-Renewing Subscription | noble.50.ios.lite.huajiao.com


## Controlling Keys

Key | comment
---- | ----
econ_global_switch_superfast | 全局经济系统开关
live_seed_switch_superfast | 直播资源只获取图片
banner_switch_superfast | 云控关闭广场banner
login_qq_superfast | qq登录开关，默认关闭
econ_luckymoney_switch_superfast | 红包开关 默认0， 1打开
econ_charge_view_config_superfast | “用花椒币购买”按钮显示云控 1显示. 购买提示
bangdan_showing_config_superfast | 云控什么榜单显示
double_type_money_switch_superfast | 双币功能开启 取值范围，0：不开启；1：开启
rate_appstore_superfast | 去App Store评分开关。默认为0，开为1；
