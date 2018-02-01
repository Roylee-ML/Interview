## 个人简历

* 孟亮，男，1989年生
* 手机号码：15841106276
* Email：[roylee.stillway@gmail.com](roylee.stillway@gmail.com)
* Github：[https://github.com/Roylee-ML](https://github.com/Roylee-ML)
* 工作经验：2 年半
* 教育经历：上东建筑大学肄业，北京蓝鸥科技 iOS 培训
* 求职意向：iOS 开发工程师
* 期望薪资：22k+

## 工作经历 

* 北京九州云动科技有限公司 （2016.10 至今）
* 微巨星（北京）管理有限公司 （2015.10 - 2016.09）

## 项目经历

两年内全程参与多个项⽬，负责的主要项⽬如下：

#### 1.省钱快报 （2016.12 至今）

项目中的职责内容

* 最初负责整个项目框架的搭建，决定技术选型方向
* 单一工程采用多 target 配合 xconfig 的方式，实现多应用开发管理（省钱快报 Pro，省钱快报探索版，好便宜等）
* 列表滑动性能优化，文本控件引入 YYLabel，采用 Model Storage 存储布局 layout，实现异步渲染
* 引入新技术 IGListKit，实现界面的数据驱动，同时，很好的解决了 UI 异步渲染导致的闪烁问题
* 网络库的两次升级
	- 项目初期，果断放弃旧项目中简单封装的网络库，建立集约式网络框架，由 APIHelper 统一管理 API、HttpClient 统一管理网络事务
	- 后期随着项目业务的增加，集约型的网络框架显露弊端，后对网络库进行升级，采用分布式的方式处理网络事务，为组件化开发做准备
* 推进组件化进程，调研、分享组件化相关知识（[总结分享资料](https://github.com/Roylee-ML/Interview/blob/master/model_source.md)），制定组件化方案，抽离开发底层库，目前正在进行底层库的迁移，下面是部分底层库
	- [SQNavigationController](https://github.com/Roylee-ML/SQNavigationController) 全屏滑动返回导航控制器，无侵入自动创建非过渡式导航条，采用 NSProxy 实现自定义属性对 UIAppearance 的支持
	- [SQNetwork](https://github.com/Roylee-ML/SQNetwork) 对 YTKNetwork 进行改进的分布式网络框架
* 客服消息体系采用多播委托机制实现消息分发，利用中间人 Proxy 管理消息监听者的内存引用

#### 2.半糖 （2016.10 - 2017.03）

项目中的职责内容

* Model 层优化，采用第三方框架替换手动 JSON 解析模式，增加 Model 职能，处理基本业务逻辑（类似胖 Model）
* 引入新技术 ReactiveCocoa、JSPatch 等
* 实现 Today Widget 与主 App 的数据共享，优化 Widget 数据同步更新
* 使用 UIScrollView 实现重用机制，构建轻量级的 CollectionView
* 全局统一 Theme 管理 UI 元素

#### 3.微巨星 （2015.10 - 2016.09）

项目中的职责内容

* 独立开发整个项目，从 0 到 1
* MVC 方式搭建主体框架，部分模块配合 MVVM 使用
* 封装 AVPlayer 实现视频播放，自定义转场效果支持横竖屏切换

## 开源

#### [SwipeTableView](https://github.com/Roylee-ML/SwipeTableView) （1.3k+ star）

实现半糖、美丽说等首页效果，具有公共 Header 的横滑组件

* 2.0 版本之前采用 UIKit Dynamic 实现公共 header 的联动效果，3.0 采用更友好的方式实现，很好的支持了 UITableView。目前，开源了 [HBHybridCollectionView](https://github.com/Roylee-ML/HBHybridCollectionView) 作为 UICollectionView 的替代方案
* [博客文章](http://error408.com/2016/07/14/SwipeTableView/)曾被 CocoaChina、简书推荐

#### [PrismaSimpleImagePicker](https://github.com/Roylee-ML/PrismaSimpleImagePicker)

Swift 仿写的 Prisma iOS 客户端

* 曾上过 github trending oc 榜数日
* AVFoundation 实现自定义相机，Photos 实现相册采集





