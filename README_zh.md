Tuya iOS Smart Planter Sample
========================
[English](README.md)

功能概述
------------------------

Tuya iOS Smart Planter Sample 提供简单示例用于对智能WiFi植物生长机的远程控制以及数据监测,该植物生长机基于Tuya IoTOS Embeded WiFi &Ble SDK实现。

Tuya iOS Smart Planter Sample 已实现以下功能：

- 用户管理模块(注册、登录、重置密码)
- 默认家庭创建
- 设备配网模块(EZ配网模式)
- 设备控制模块(植物生长机开关、风速控制、温湿度监测、土壤湿度、光照等)

### 相关硬件和嵌入式项目

- 智能WiFi植物生长机Demo的详细介绍文档，请参考涂鸦Demo中心：[https://developer.tuya.com/cn/demo/smart-planter](https://developer.tuya.com/cn/demo/smart-planter)

- Tuya IoTOS Embeded Demo WiFi & BLE Smart-Planter 项目 Github 仓库: [https://github.com/tuya/tuya-iotos-embeded-demo-wifi-ble-smart-planter/blob/master/README_zh.md](https://github.com/tuya/tuya-iotos-embeded-demo-wifi-ble-smart-planter/blob/master/README_zh.md)

- 开发板套件相关详情请参考：[三明治开发套件](https://developer.tuya.com/cn/docs/iot/device-development/tuya-development-board-kit/tuya-sandwich-evaluation-kits/-tuya-sandwich-evaluation-kits?id=K97o0ixytemvr)

先决条件
------------------------

1.Xcode 12.0 and later

2.iOS 12 and later

开始
------------------------

#### 一、项目配置

1、根据[准备工作](https://developer.tuya.com/cn/docs/app-development/preparation/preparation?id=Ka69nt983bhh5)文档说明，注册涂鸦开发者账号，并完成应用的创建，将Sample的包名替换成创建时设置的包名。

2、根据[集成SDK](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/integrate-sdk?id=Ka5d52ewngdoi)文档说明，集成安全图片以及重新设置AppKey和AppSecret。

#### 二、界面

在完成以上项目配置后，运行程序，App展示各个界面如下：

|                             首页                             |                             注册                             |                             登录                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0891.PNG" alt="7f02e6c5e6654a882713361ae88a679c" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0894.PNG" alt="062740ed7623c6fbb7220742e2e01d4d" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0892.PNG" alt="b6f57d71a6a114676585cee34ab29abe" style="zoom:20%;" /> |
|                           重置密码                           |                             主页                             |                           用户信息                           |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0893.PNG" alt="a33ffb858ea3f3299a0f661d6a8e965c" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0890.PNG" alt="8bd282665945cf600bce2ae173cd5ddd" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0899.PNG" alt="5522fbc1d3735be6db9a365e47a8ce44" style="zoom:20%;" /> |
|                            EZ配网                            |                           设备列表                           |                           控制面板                           |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0897.PNG" alt="ca90caaa492e99c5afa4d41bdf0de309" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0900.PNG" alt="5946494f90544ed818ce4e0c7b9e90d5" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0898.PNG" alt="3cc502c2bfdfd7585606536abde102cd" style="zoom:20%;" /> |
|                            创建家庭                            |                                                      |                                                      |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0896.PNG" alt="ca90caaa492e99c5afa4d41bdf0de309" style="zoom:20%;" /> | 

 

#### 三、用户管理模块

用户管理模块涉及到用户注册登录以及密码重置，关于用户管理更多信息说明以及Api接口调用，请查阅[用户管理](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/user?id=Ka5cgmm97jlt2)。

##### 3.1、获取验证码

```objc
// phone
[[TuyaSmartUser sharedInstance] sendVerifyCode:@"your_country_code" phoneNumber:@"your_phone_number" type:1 success:^{
    NSLog(@"sendVerifyCode success");
} failure:^(NSError *error) {
    NSLog(@"sendVerifyCode failure: %@", error);
}];

// email
[[TuyaSmartUser sharedInstance] sendVerifyCodeByRegisterEmail:@"your_country_code" email:@"your_email" success:^{
  	NSLog(@"sendVerifyCode success");
} failure:^(NSError *error) {
    NSLog(@"sendVerifyCode failure: %@", error);
}];
```
##### 3.2、用户注册

```objc
// phone
[[TuyaSmartUser sharedInstance] registerByPhone:@"your_country_code" phoneNumber:@"your_phone_number" password:@"your_password" code:@"verify_code" success:^{
    NSLog(@"register success");
} failure:^(NSError *error) {
    NSLog(@"register failure: %@", error);
}];

// email 
[[TuyaSmartUser sharedInstance] registerByEmail:@"your_country_code" email:@"your_email" password:@"your_password" code:@"verify_code" success:^{
    NSLog(@"register success");
} failure:^(NSError *error) {
    NSLog(@"register failure: %@", error);
}];
```

##### 3.3、用户登录

```java
// phone
[[TuyaSmartUser sharedInstance] loginByPhone:@"your_country_code" phoneNumber:@"your_phone_number" password:@"your_password" success:^{
		NSLog(@"login success");
} failure:^(NSError *error) {
		NSLog(@"login failure: %@", error);
}];
// email
[[TuyaSmartUser sharedInstance] loginByEmail:@"your_country_code" email:@"your_email" password:@"your_password" success:^{
    NSLog(@"login success");
} failure:^(NSError *error) {
    NSLog(@"login failure: %@", error);
}];
```

##### 3.4、重置密码

```objc
// phone
[TuyaSmartUser sharedInstance] resetPasswordByPhone:@"your_country_code" phoneNumber:@"your_phone_number" newPassword:@"your_password" code:@"verify_code" success:^{
		NSLog(@"resetPasswordByPhone success");
	} failure:^(NSError *error) {
		
// email
[TuyaSmartUser sharedInstance] resetPasswordByEmail:@"your_country_code" email:@"your_email" newPassword:@"your_password" code:@"verify_code" success:^{
		NSLog(@"resetPasswordByEmail success");
	} failure:^(NSError *error) {
		NSLog(@"resetPasswordByEmail failure: %@", error);
	}];
```
##### 3.5、用户登出

```java
[TuyaSmartUser sharedInstance] loginOut:^{
	NSLog(@"logOut success");
} failure:^(NSError *error) {
	NSLog(@"logOut failure: %@", error);
}];});
```

> 如果在注册或者登录的时候提示权限不足，请检查是否正确完成了项目配置步骤。

#### 四、家庭管理模块

涂鸦设备在添加之前，需要创建家庭，本Demo仅在程序启动的时候，根据用户的手机信息创建了一个默认家庭，关于家庭管理的更多信息以及相关Api接口，请查阅[家庭管理](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/home?id=Ka5d52ey6e58h)。

##### 4.1、获取家庭列表

```objc
[self.homeManager getHomeListWithSuccess:^(NSArray<TuyaSmartHomeModel *> *homes) {
        // homes 家庭列表
    } failure:^(NSError *error) {
        NSLog(@"get home list failure: %@", error);
    }];
```

##### 4.2、创建家庭

```objc
[self.homeManager addHomeWithName:@"you_home_name"
                          geoName:@"city_name"
                            rooms:@[@"room_name"]
                         latitude:lat
                        longitude:lon
                          success:^(double homeId) {

        // homeId 创建的家庭的 homeId
        NSLog(@"add home success");
    } failure:^(NSError *error) {
        NSLog(@"add home failure: %@", error);
    }];
```

##### 4.3、获取家庭的详细信息

```objc
self.home = [TuyaSmartHome homeWithHomeId:homeId];
	[self.home getHomeDetailWithSuccess:^(TuyaSmartHomeModel *homeModel) {
        // homeModel 家庭信息
        NSLog(@"get home detail success");
    } failure:^(NSError *error) {
        NSLog(@"get home detail failure: %@", error);
    }];
```

##### 4.4、修改家庭信息

```objc
self.home = [TuyaSmartHome homeWithHomeId:homeId];
    [self.home updateHomeInfoWithName:@"new_home_name" geoName:@"city_name" latitude:lat longitude:lon success:^{
        NSLog(@"update home info success");
    } failure:^(NSError *error) {
        NSLog(@"update home info failure: %@", error);
    }];
```

##### 4.5、解散家庭

```objc
[self.home dismissHomeWithSuccess:^() {
        NSLog(@"dismiss home success");
    } failure:^(NSError *error) {
        NSLog(@"dismiss home failure: %@", error);
    }];
```





#### 五、设备配网模块

智能WiFi植物生长机支持WiFi模式下EZ配网、AP配网，更多设备配网信息以及API接口，请查阅[设备配网](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/activator?id=Ka5cgmlzpfig4)。

开始配网之前，SDK 需要在联网状态下从涂鸦云获取配网 Token，Token 的有效期为10分钟，且配置成功后就会失效（再次配网需要重新获取）。

##### 5.1、配网 Token 获取接口
```objc
- (void)getTokenWithHomeId:(long long)homeId
                   success:(TYSuccessString)success
                   failure:(TYFailureError)failure;
```
**参数说明**

| 参数   | 说明                      |
| :----- | :------------------------ |
| homeId | 设备将要绑定到的家庭的 Id |
| success   | 成功回调，返回配网 Token |
| failure | 失败回调，返回失败原因 |


##### 5.2、开始配网接口
```objc
- (void)startConfigWiFi:(TYActivatorMode)mode
                   ssid:(NSString *)ssid
               password:(NSString *)password
                  token:(NSString *)token
                timeout:(NSTimeInterval)timeout;
```
**参数说明**

| 参数   | 说明                      |
| :----- | :------------------------ |
| mode | 配网模式 |
| ssid   | Wi-Fi 名称 |
| password | Wi-Fi 密码 |
| token | 配网 Token |
| timeout | 超时时间，默认 100 秒 |


##### 5.3、配网代理回调
```objc
- (void)activator:(TuyaSmartActivator *)activator didReceiveDevice:(TuyaSmartDeviceModel *)deviceModel error:(NSError *)error;
```
**参数说明**

| 参数   | 说明                      |
| :----- | :------------------------ |
| activator | 配网使用 TuyaSmartActivator 对象实例 |
| deviceModel   | 配网成功时，返回此次配网的设备模型，失败时返回 nil |
| error | 配网失败时，标示错误信息，成功时为 nil |


##### 5.4、停止配网
```objc
- (void)stopConfigWiFi;
```



#### 六、设备管理

当设备配网成功后，可以在设备列表查看到已配网的植物生长机设备，选中设备，进入控制面板,关于设备更多信息以及API接口请查阅[设备管理](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/device?id=Ka5cgmmjr46cp)。

##### 6.1、设备初始化

注意：需要通过 TuyaSmartHome 初始化一个 home 实例，然后调用接口 getHomeDetailWithSuccess:failure: 获取家庭的详情，同步过家庭的详情后，初始化设备才能成功。

错误的设备 id 可能会导致初始化失败，此时设备的实例返回 nil

```objc
/**
 *  Get TuyaSmartDevice instance. If current user don't have this device, a nil will be return.
 *  获取设备实例。如果当前用户没有该设备，将会返回nil。
 *
 *  @param devId Device ID
 *  @return instance
 */
+ (nullable instancetype)deviceWithDeviceId:(NSString *)devId;
```


##### 6.2、设备代理监听

```objc
- (void)initDevice {
    self.device = [TuyaSmartDevice deviceWithDeviceId:@"your_device_id"];
    self.device.delegate = self;
}

#pragma mark - TuyaSmartDeviceDelegate

- (void)device:(TuyaSmartDevice *)device dpsUpdate:(NSDictionary *)dps {
    // 设备的 dps 状态发生变化，刷新界面 UI
}

- (void)deviceInfoUpdate:(TuyaSmartDevice *)device {
    //当前设备信息更新 比如 设备名称修改、设备在线离线状态等
}

- (void)deviceRemoved:(TuyaSmartDevice *)device {
    //当前设备被移除
}

- (void)device:(TuyaSmartDevice *)device signal:(NSString *)signal {
    // Wifi信号强度
}

- (void)device:(TuyaSmartDevice *)device firmwareUpgradeProgress:(NSInteger)type progress:(double)progress {
    // 固件升级进度
}

- (void)device:(TuyaSmartDevice *)device firmwareUpgradeStatusModel:(TuyaSmartFirmwareUpgradeStatusModel *)upgradeStatusModel {
    // 设备升级状态的回调
}
```

##### 6.3、设备控制

设备控制接口功能为向设备发送功能点，来改变设备状态或功能。
设备控制支持三种通道控制，局域网控制，云端控制和自动方式（如果局域网在线，先走局域网控制，局域网不在线，走云端控制）

设备功能点说明: 
TuyaSmartDeviceModel 类的 dps 属性（NSDictionary 类型）定义了当前设备的状态，称作数据点（DP 点）或功能点
dps 字典里的每个 key 对应一个功能点的 dpId，value 对应一个功能点的 dpValue ，dpValue 为该功能点的值

发送控制指令按照以下格式：
{"<dpId>":"<dpValue>"}

```objc
局域网控制：
[self.device publishDps:dps mode:TYDevicePublishModeLocal success:^{
		NSLog(@"publishDps success");
	} failure:^(NSError *error) {
		NSLog(@"publishDps failure: %@", error);
	}];

云端控制：
[self.device publishDps:dps mode:TYDevicePublishModeInternet success:^{
		NSLog(@"publishDps success");
	} failure:^(NSError *error) {
		NSLog(@"publishDps failure: %@", error);
	}];
	
自动控制：
[self.device publishDps:dps mode:TYDevicePublishModeAuto success:^{
		NSLog(@"publishDps success");
	} failure:^(NSError *error) {
		NSLog(@"publishDps failure: %@", error);
	}];
```
植物生长机DP控制点：

1.开关：启动、关闭设备

2.水箱抽水水泵开关：在设备启动后，开启水泵，可以往水箱中注水

3.当前温度、湿度显示

4.灯光定时：控制灯照时间

5.灯光倒计时

6.故障告警：展示故障代码

7.设置最大温度：当温度高于最大温度时，光照关闭，风扇会启动

8.设置最大湿度：当湿度高于最大湿度时，风扇会启动

9.水箱容积

10.设置光照颜色

11.设置最小温度：当温度低于最小温度时，光照打开

12.设置最小湿度：当湿度低于最小湿度时，土壤水泵会打开，从水箱中给植物浇水

13.自动光照开关

14.移除设备开关：移除当前配网设备，使设备重新进入配网模式



##### 6.4、设备移除

设备被移除后，会重新进入待配网状态（快连模式）

```objc
- (void)remove:(nullable TYSuccessHandler)success failure:(nullable TYFailureError)failure;
```

##### 6.5、恢复出厂设置

设备恢复出厂设置后，会重新进入待配网状态（快连模式），设备的相关数据会被清除掉

```objc
- (void)resetFactory:(nullable TYSuccessHandler)success failure:(nullable TYFailureError)failure;
```



#### 七、DIY 

通过智能植物生长机的控制面板可以看到，我们可以对植物生长机的开关、温度、湿度等信息进行监测和控制，在此基础上，开发者可以通过设置不同场景来对设备进行不同diy操作,比如你可以设置一个场景，当温度大于30摄氏度时候自动打开水泵开关。




问题反馈
------------------------

您可以通过**Github Issue** 或通过[**工单**](https://service.console.tuya.com)来进行反馈您所碰到的问题

LICENSE
------------------------
Tuya iOS Smart Planter Sample是在MIT许可下提供的。更多信息请参考[LICENSE](LICENSE)文件
