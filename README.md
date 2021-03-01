Tuya iOS Smart Planter Sample
========================
[中文版](README_zh.md) 

Functions overview
------------------------

The Tuya IOS Smart Planter Sample provides a simple example for remote control and data monitoring of the Smart WiFi plant growth machine, which is built on the Tuya Iotos Embeded WiFi &Ble SDK.

The Tuya IOS Smart Planter Sample has realized the following functions:

- User management module (registration, login, password reset)
- Default family creation
- Equipment distribution network module (EZ distribution network mode)
- Equipment control module (plant growth machine switch, wind speed control, temperature and humidity monitoring, soil moisture, lighting, etc.)

### Related Hardware & Tuya IoTOS Embedded Github Demo

- For Smart WiFi Plant Growth Machine Demo documentation，please check Tuya Demo Center：[https://developer.tuya.com/en/demo/smart-planter](https://developer.tuya.com/cn/demo/smart-planter)

- Tuya IoTOS Embedded Demo WiFi & BLE Smart-Planter Github Repo link: [https://github.com/tuya/tuya-iotos-embeded-demo-wifi-ble-smart-planter/blob/master/README_zh.md](https://github.com/tuya/tuya-iotos-embeded-demo-wifi-ble-smart-planter/blob/master/README_zh.md)

- Evaluation Kits：[Sandwich Evaluation Kits](https://developer.tuya.com/en/docs/iot/device-development/tuya-development-board-kit/tuya-sandwich-evaluation-kits/-tuya-sandwich-evaluation-kits?id=K97o0ixytemvr)


Prerequisites
------------------------

1.Xcode 12.0 and later

2.iOS 12 and later

Start
------------------------

#### I.Project configuration

1.According to the [Preparation](https://developer.tuya.com/cn/docs/app-development/preparation/preparation?id=Ka69nt983bhh5) documentation,register the Doodle Developer account and complete the creation of the application, replacing the package name of Sample with the package name set at creation time.

2.According to the [Integration SDK](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/integrate-sdk?id=Ka5d52ewngdoi) documentation,Integrate security images and reset AppKey and AppSecret.

#### II.Interface

After completing the above project configuration, run the program, and the APP displays each interface as follows:

|                             FirstPage                             |                             Register                             |                             Login                             |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0901.PNG" alt="7f02e6c5e6654a882713361ae88a679c" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0902.PNG" alt="062740ed7623c6fbb7220742e2e01d4d" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0903.PNG" alt="b6f57d71a6a114676585cee34ab29abe" style="zoom:20%;" /> |
|                           Reset Password                           |                             HomePage                             |                           User Information                           |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0904.PNG" alt="a33ffb858ea3f3299a0f661d6a8e965c" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0905.PNG" alt="8bd282665945cf600bce2ae173cd5ddd" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0906.PNG" alt="5522fbc1d3735be6db9a365e47a8ce44" style="zoom:20%;" /> |
|                            EZ Mode                            |                           Device List                           |                           Control Panel                           |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0907.PNG" alt="ca90caaa492e99c5afa4d41bdf0de309" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0908.PNG" alt="5946494f90544ed818ce4e0c7b9e90d5" style="zoom:20%;" /> | <img src="https://images.tuyacn.com/app/Hanh/IMG_0909.PNG" alt="3cc502c2bfdfd7585606536abde102cd" style="zoom:20%;" /> |
|                            New Home                            |                                                      |                                                      |
| <img src="https://images.tuyacn.com/app/Hanh/IMG_0910.PNG" alt="ca90caaa492e99c5afa4d41bdf0de309" style="zoom:20%;" /> | 

 

#### III.User Management Module

User management module involves user registration, login and password reset. For more information about user management and API interface call, please refer to [User Management](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/user?id=Ka5cgmm97jlt2)。

##### 3.1 Get verifyCode

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
##### 3.2 User registration

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

##### 3.3 User login

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

##### 3.4 Reset password

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
##### 3.5 User logout

```java
[TuyaSmartUser sharedInstance] loginOut:^{
	NSLog(@"logOut success");
} failure:^(NSError *error) {
	NSLog(@"logOut failure: %@", error);
}];});
```

> If you are warned of insufficient permissions when registering or logging in, check that you have completed the project configuration steps correctly.

#### Ⅳ.Home Management Module

Before the Tuya device is added, a family needs to be created. This Demo only creates a default family according to the user's mobile phone information when the program is started. For more information about family management and related API interfaces, please refer to [Home Management](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/home?id=Ka5d52ey6e58h)。

##### 4.1 Get family list

```objc
[self.homeManager getHomeListWithSuccess:^(NSArray<TuyaSmartHomeModel *> *homes) {
        // homes Family List
    } failure:^(NSError *error) {
        NSLog(@"get home list failure: %@", error);
    }];
```

##### 4.2 New home

```objc
[self.homeManager addHomeWithName:@"you_home_name"
                          geoName:@"city_name"
                            rooms:@[@"room_name"]
                         latitude:lat
                        longitude:lon
                          success:^(double homeId) {

        // homeId 
        NSLog(@"add home success");
    } failure:^(NSError *error) {
        NSLog(@"add home failure: %@", error);
    }];
```

##### 4.3 Get family details

```objc
self.home = [TuyaSmartHome homeWithHomeId:homeId];
	[self.home getHomeDetailWithSuccess:^(TuyaSmartHomeModel *homeModel) {
        // homeModel  Family Details
        NSLog(@"get home detail success");
    } failure:^(NSError *error) {
        NSLog(@"get home detail failure: %@", error);
    }];
```

##### 4.4 Modify family information

```objc
self.home = [TuyaSmartHome homeWithHomeId:homeId];
    [self.home updateHomeInfoWithName:@"new_home_name" geoName:@"city_name" latitude:lat longitude:lon success:^{
        NSLog(@"update home info success");
    } failure:^(NSError *error) {
        NSLog(@"update home info failure: %@", error);
    }];
```

##### 4.5 Dissolve family

```objc
[self.home dismissHomeWithSuccess:^() {
        NSLog(@"dismiss home success");
    } failure:^(NSError *error) {
        NSLog(@"dismiss home failure: %@", error);
    }];
```





#### V.Network Module

Intelligent WIFI plant growth machine supports EZ distribution network and AP distribution network under WIFI mode. For more equipment distribution network information and API interface, please refer to [Network Module](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/activator?id=Ka5cgmlzpfig4)。

Before network distribution, the SDK needs to obtain the distribution network Token from the Tuya Cloud in the networking state. The Token is valid for 10 minutes and will become invalid after successful configuration (the distribution network needs to be acquired again).

##### 5.1 Network token access
```objc
- (void)getTokenWithHomeId:(long long)homeId
                   success:(TYSuccessString)success
                   failure:(TYFailureError)failure;
```
**Parameters explain**

| Parameters   | explain                      |
| :----- | :------------------------ |
| homeId | The ID of the home to which the device will bind |
| success   | Successful callback returns the distribution network Token |
| failure | A failure callback that returns the reason for the failure |


##### 5.2 Start configuring the network
```objc
- (void)startConfigWiFi:(TYActivatorMode)mode
                   ssid:(NSString *)ssid
               password:(NSString *)password
                  token:(NSString *)token
                timeout:(NSTimeInterval)timeout;
```
**Parameters explain**

| Parameters   | explain                      |
| :----- | :------------------------ |
| mode | Distribution network model |
| ssid   | Wi-Fi name |
| password | Wi-Fi password |
| token | Distribution network Token |
| timeout | Timeout time, default 100 seconds |


##### 5.3 Distribution network agent callback
```objc
- (void)activator:(TuyaSmartActivator *)activator didReceiveDevice:(TuyaSmartDeviceModel *)deviceModel error:(NSError *)error;
```
**Parameters explain**

| Parameters   | explain                      |
| :----- | :------------------------ |
| activator | The distribution network uses the Tuyasmartactivator object instance |
| deviceModel   | When the distribution network is successful, the device model of the distribution network is returned; when it fails, nil is returned |
| error | When the distribution network fails, the error message is marked, and when it succeeds, it is nil |


##### 5.4 Stop the distribution network
```objc
- (void)stopConfigWiFi;
```



#### VI.Equipment management

When the equipment is successfully networked, you can view the networked plant growth machine equipment in the device list. Select the device and enter the control panel. For more information about the device and the API interface, please refer to [Equipment management](https://developer.tuya.com/cn/docs/app-development/ios-app-sdk/device?id=Ka5cgmmjr46cp)。

##### 6.1 Device initialization

Note: need to TuyaSmartHome initialize a home as an example, and then call interface getHomeDetailWithSuccess: failure: for details of the family, after synchronization family details, initialize the equipment to be successful.

The wrong device ID may cause initialization to fail, in which case the instance of the device returns nil

```objc
/**
 *  Get TuyaSmartDevice instance. If current user don't have this device, a nil will be return.
 *  Get the device instance. If the current user does not have the device, nil will be returned.
 *
 *  @param devId Device ID
 *  @return instance
 */
+ (nullable instancetype)deviceWithDeviceId:(NSString *)devId;
```


##### 6.2 Device agent monitoring

```objc
- (void)initDevice {
    self.device = [TuyaSmartDevice deviceWithDeviceId:@"your_device_id"];
    self.device.delegate = self;
}

#pragma mark - TuyaSmartDeviceDelegate

- (void)device:(TuyaSmartDevice *)device dpsUpdate:(NSDictionary *)dps {
    // The DPS status of the device changes, and the UI of the interface is refreshed
}

- (void)deviceInfoUpdate:(TuyaSmartDevice *)device {
    //Current device information update, such as device name change, device online and offline status, etc
}

- (void)deviceRemoved:(TuyaSmartDevice *)device {
    //The current device has been removed
}

- (void)device:(TuyaSmartDevice *)device signal:(NSString *)signal {
    // WIFI Signal Strength
}

- (void)device:(TuyaSmartDevice *)device firmwareUpgradeProgress:(NSInteger)type progress:(double)progress {
    // Firmware upgrade progress
}

- (void)device:(TuyaSmartDevice *)device firmwareUpgradeStatusModel:(TuyaSmartFirmwareUpgradeStatusModel *)upgradeStatusModel {
    // A callback to the device upgrade status
}
```

##### 6.3 Device control

The function of the device control interface is to send function points to the device to change the device state or function.
Device control supports three channel control, LAN control, cloud control and automatic mode (if LAN is online, LAN control first, LAN is not online, cloud control)

Description of equipment function points:
The DPS property of the TuyasmartDeviceModel class (type NSDictionary) defines the state of the current device, called a data point (DP point) or function point
Each key in the DPS dictionary corresponds to the dPID of a function point, and the value corresponds to the dpValue of a function point, and dpValue is the value of the function point

Control instructions are sent in the following format:
{"<dpId>":"<dpValue>"}

```objc
LAN control:
[self.device publishDps:dps mode:TYDevicePublishModeLocal success:^{
		NSLog(@"publishDps success");
	} failure:^(NSError *error) {
		NSLog(@"publishDps failure: %@", error);
	}];

Cloud control:
[self.device publishDps:dps mode:TYDevicePublishModeInternet success:^{
		NSLog(@"publishDps success");
	} failure:^(NSError *error) {
		NSLog(@"publishDps failure: %@", error);
	}];
	
Automatic control:
[self.device publishDps:dps mode:TYDevicePublishModeAuto success:^{
		NSLog(@"publishDps success");
	} failure:^(NSError *error) {
		NSLog(@"publishDps failure: %@", error);
	}];
```
DP control points of plant growth machine:

1. Switch: start and close the device

2. Water tank pumping pump switch: after the equipment is started, turn on the water pump to fill the water tank

3. Current temperature and humidity display

4. Timing of lights: control the lighting time

5. Light countdown

6. Fault warning: display the fault code

7. Set the maximum temperature: when the temperature is higher than the maximum temperature, the light will turn off and the fan will start

8. Set the maximum humidity: when the humidity is higher than the maximum humidity, the fan will start

9. Water tank volume

10. Set light colors

11. Set the minimum temperature: When the temperature is below the minimum temperature, the light turns on

12. Set the minimum humidity: When the humidity is below the minimum humidity, the soil pump will be turned on to water the plants from the tank

13. Automatic light switch

14. Device removal switch: remove the current distribution network equipment, so that the equipment into the distribution network mode again



##### 6.4 Equipment remove

After the device is removed, it will re-enter the state of pending network (fast connection mode).

```objc
- (void)remove:(nullable TYSuccessHandler)success failure:(nullable TYFailureError)failure;
```

##### 6.5 Factory data reset

After the factory setting is restored, the device will re-enter the state of the pending network (fast connection mode), and the relevant data of the device will be erased

```objc
- (void)resetFactory:(nullable TYSuccessHandler)success failure:(nullable TYFailureError)failure;
```



#### VII.DIY 

Through smart plant growth machine control panel you can see, we can switch on plant growth machine, temperature and humidity monitoring and control of information, on this basis, the developer can set different scenarios to diy different operating equipment, you can set a scene, for example, when more than 30 degrees Celsius temperature automatically open water pump switch.




The problem of feedback
------------------------

You can use the**Github Issue** or [**ticket**](https://service.console.tuya.com) to provide feedback on any problems you encounter

LICENSE
------------------------
The Tuya IOS Smart Planter Sample is provided under the MIT license. See the [LICENSE](LICENSE) file for more information
