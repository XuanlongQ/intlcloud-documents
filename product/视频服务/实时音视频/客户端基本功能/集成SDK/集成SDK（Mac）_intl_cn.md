本文将指导您完成在 Mac 端下实时音视频客户端功能的 SDK 集成。
## 源码下载
在此我们提供以下所讲到的完整 Demo 代码，如有需要请您自行下载。
[Demo 代码下载](http://dldir1.qq.com/hudongzhibo/ILiveSDK/Demo/MAC_TRTC.zip)
## 操作步骤
### 创建 Mac 工程
如果您已经有一个工程待集成，请直接跳到下一步 [集成 SDK](https://cloud.tencent.com/document/product/647/19554)。
首先，使用 Xcode 创建一个新的工程用来集成我们的 SDK。
打开 Xcode，【 File 】-【 New 】-【 Project 】：
![](https://main.qcloudimg.com/raw/07cdd8293bdeb83e0be5bd2452f6a06e.png)
选择macOS ->【 Cocoa App 】
![](https://main.qcloudimg.com/raw/d78e4346ec09d699fc8af3afb48e3337.png)
设置工程名为TRTCMac集成 SDK，语言选择为 Objective-C，Team、Organization Name 和 Organization Identifier 根据自身情况填写（也可随便填写）,然后选择下一步选择项目存放地址，单击 【 create 】即可 。
#### 集成 SDK
#### 获取SDK
Mac版 ILiveSDK 包含如下一些子 SDK：
- IMSDK：提供 IM 即时通信功能
- AVSDK：提供底层音视频功能
- ILiveSDK：在 AVSDK 基础上封装而成，提供更简单易用的音视频功能接口

我们先在工程目录中新建一个名为 FrameworksMac 的文件夹，用来存放我们的 SDK，由于 ILiveSDK 包含若干个子 SDK，所以我们提供了一个 [SDK 下载脚本](http://dldir1.qq.com/hudongzhibo/ILiveSDK/LoadSDK.sh)方便获取所有的SDK。
单击下载脚本，将其放置于刚才创建的 FrameworksMac 文件夹下：
![](https://main.qcloudimg.com/raw/c2abae1c483861e7c8117d25673d1915.png)
运行下载脚本（ 打开终端，cd 命令进入 FrameworksMac 目录下，运行命令 sh LoadSDK.sh ），就会自动下载所有SDK，下载完成之后会自动解压，并删除下载的压缩包，稍等片刻即可。
#### 导入SDK
下载完成后，我们需将 SDK 导入工程，在工程根目录上单击右键->【 Add Files to "TRTCMac" 】：
![](https://main.qcloudimg.com/raw/fda07853f441f7838717ef065b11f84f.png)
在弹出的目录选择框中选择我们刚刚创建的【 FrameworksMac 文件夹 】->【 Add 】：
![](https://main.qcloudimg.com/raw/2d5cdd40be02fce97889e40971f8aa6b.png)
添加完成后的工程目录：
![](https://main.qcloudimg.com/raw/a3a3c5861d56dad4150cda6608af6a85.png)　　
#### 添加系统依赖库
ILiveSDK 中的 SDK 依赖了一些系统库，我们还需要将这些系统库添加到项目中来。
单击【 项目文件 】->【 targets 】->【 Genaeral 】- 拉到最下面的 Linked Frameworks and Libraries 区域 -> 单击【 + 】号 -> 输入系统库名称 -> 单击【 add 】添加。
![](https://main.qcloudimg.com/raw/6afac63510536fe9d4542ab8a38425ca.png)
需添加的系统库清单
- libsqlite3.tbd
- libiconv.tbd
- libstdc++.6.tbd
- libc++.tbd
- libz.tbd
- libresolve.9.tbd
- CoreWLAN.framework
- QuartzCore.framework
- QAVSDK.framework
- TLSSDK.framework
- QALSDK.framework
- ILiveSDK.framework
- IMCore.framework
- IliveLogReport.framework
- TILFilterSDK.framework
- ImSDK.framework

添加系统库后，项目中会多出一个 Frameworks 文件夹，里面放的就是我们添加的系统库，由于需要添加的系统库较多，一个方便的方法是，直接在文末下载我们给出的 Demo 代码（[单击下载](http://dldir1.qq.com/hudongzhibo/ILiveSDK/Demo/iOS/demo_import.zip)），将其中的系统库直接拖拽到您的工程中（ 从 Frameworks 文件夹直接拖到您的项目的 Linked Frameworks and Libraries 区域 ）。
#### 工程配置
为了能够正常使用 SDK，还需要进行一些工程配置：
-ObjC 配置
【 Build Settings 】 -> 【 Other Linker Flags 】 -> 【 -ObjC （注意大小写）】：
![](https://main.qcloudimg.com/raw/3a8c59d55d750e13260809e83d5b6029.png)

#### 运行检查
如果以上步骤均无错误，这时我们就能正常使用 ILiveSDK 了，在 ViewController.m 的 viewDidLoad 函数中添加获取版本号的代码：
```
//导入头文件
#import <ILiveSDK/ILiveCoreHeader.h>

//获取版本号
NSLog(@"ILiveSDK version:%@",[[ILiveSDK getInstance] getVersion]);
NSLog(@"AVSDK version:%@",[QAVContext getVersion]);
NSLog(@"IMSDK version:%@",[[TIMManager sharedInstance] GetVersion]);

//打印结果
2018-09-03 11:49:28.060945+0800 TRTCMac[73399:23447259] ILiveSDK version:1.9.3.13966
2018-09-03 11:49:28.060956+0800 TRTCMac[73399:23447259] AVSDK version:1.9.9.1012.Local
2018-09-03 11:49:28.060969+0800 TRTCMac[73399:23447259] IMSDK version:v2.5.4.10421.10420
```
恭喜，至此说明ILiveSDK已经成功集成。
## 联系邮箱
如果对上述文档有不明白的地方，请反馈到trtcfb@qq.com
