# 组件化总结

<br>
## 索引
1. [组件化方案](https://coding.net/u/roylee/p/Interview/git/blob/master/model_source.md#组件化方案)
2. [私有 PodSpec](https://coding.net/u/roylee/p/Interview/git/blob/master/model_source.md#私有-podspec)


## 组件化方案

### 组件化的使用场景

组件化的出现是为了解决复杂的项目结构，将大型项目拆分细化为单一模块，从而便于维护调试开发 
### 组件化的设计

* 为了消除不同模块间的耦合，需要把不同模块拆分开来。同时不同模块间的通信需要一个中间层来负责沟通
* 中间层的设计

	- 路由设计要求是单向的，即不同的模块依赖于中间层，但是中间层不依赖于各个模块
* 采用 scheme 方式设计路由

	- 需要建立后台存放 scheme 规范文档，每个模块按照文档规范提供服务，注册 URL
	- 每个模块的 scheme 服务注册方式可以采用淘宝的思路——本地文件配置当前模块提供的服务
	- 全局路由按照规则读取各个模块的配置文件
	- 为避免模块配置添加错误，每次模块改动后，可以对路由进行单元测试：**拉取后台配置文档，遍历模块配置服务进行匹配**
* Model 层的设计

	- 苹果采用的 MVCS 提供 Store 来 format model。
	- 并且可以结合网络框架处理，做到数据分离
* 功能组件的设计原则
	- 在小范围内，单一功能单一职责，每个功能定义清晰（一个功能执行一个任务）

* 全局配置信息共享解决方案
	- 路由负责组件间通信以及各个服务的交互
	- 单独提供全局 context 来负责全局信息的共享（可以参考阿里巴巴的 BeeHive）


### 开发作业流程


* 前期可以在一个工程中构建多个平行组件文件并行开发，然后，不同组件间禁止相互调用、引用
	
	```objc
	开发工程目录结构
    .
    │   ├── MainProject
    │   │   ├── HomeComponent
    │   │   ├── CateComponent
    │   │   ├── SearchComponent
    │   │   ├── DiscoverComponent
    │   │   ├── CenterComponent
    │   │   ├── SettingComponent
    │   │   ├── LoginComponent
    │   │   ├── DetailComponent
    │   │   ├── PhotoViewerComponent
    │   │   ├── WebComponent
    │   │   ├── ShareComponent    
    │   │   └── ...
    │   └── PodProject
    │       ├── Network
    │       ├── ImageLoader
    │       ├── EventTracker
    │       ├── Cache
    │       ├── Navigation
    │       ├── Manager
    │       ├── Utility
    │       ├── PhotoViewer
    │       ├── CategoryKit
    │       ├── OhterThird
    │       └── ...
    
    ```
    
* 另外提供一个壳工程作为最终主工程打包


	```objc
	打包壳工程
    .
    │   ├── MainProject
    │   │   └── Main
    │   └── PodProject
    │       ├── Component1
    │       ├── Component2
    │       └── ...
		    
	```


### 淘宝 App 研究

* 采用配置文件来管理不同模块的映射服务，具体原理类似天猫 App 统跳协议和Rewrite引擎
* Class2PageMap.plist 存储项目类名到别名的映射 (key 类名 -> value 别名)，可能用于统计等
* MatrixConfig.plist 作为主配置文件，存储路由各个模块的 plist
* 每个模块按既定规则配置 plist 文件，淘宝采用 `模块名_boundle.plist` 的方式命名


## 私有 PodSpec


### Pod spec 使用指南：

- 创建私有 spec repo，作为存放私有仓库的远程源仓库。终端执行下面的命令：

```objc
pod repo add 'MySpecs' 'specs repo url'

// e.g. code
pod repo add Specs https://git.coding.net/roylee/Specs.git
```

- 创建私有库，并创建 pod 同名 .spec 文件，这些都是在自己的私有库开发完成验证提交时的操作，并且在当前私有库的路径下

> 执行` pod lib lint` 本地验证，`pod spec lint` 远程验证

- 添加私有库到第一步创建的私有 spec，之后就可以在自己私有仓库的源下面 pod 自己的库了

```objc
pod repo push MySpecs 私有库名称.podspec
```

- 私有库依赖私有库的处理：

	- 在 podfile 顶部添加 source  
	 
	```objc
	source 'MySpecs url link'
	source 'https://github.com/CocoaPods/Specs.git'
	```

	- 之后在 podfile 以及 s.dependency 中都是正常引用就可以了
	
	- 此时，校验当前私有库，如果失败，执行的 `pod lib lint` 需要添加 sources `pod lib lint —sources='MySpecs url link'`

	- 如果 sources 是多个，中间用逗号隔开即可


### 其他

- 允许警告，添加命令后缀


```objc
--allow-warnings
```
	
### 参考

[使用Cocoapods创建私有podspec](http://www.cocoachina.com/ios/20150228/11206.html)
	
[Private Pods](http://guides.cocoapods.org/making/private-cocoapods.html)

