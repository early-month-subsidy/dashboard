### 技术学习报告

我在团队中负责需求分析、项目总体规划和具体分工，确定项目各阶段迭代周期，负责给出各迭代周期需求建议报告和前端开发。

#### 需求描述

需求分析是软件生命周期中重要的一步，也是决定性的一步，是将系统从黑盒逐步转换为白盒的一个过程。对于整个系统而言，首先需要分析系统是否具有开发的价值和意义，其次要分析系统是否可以开发成功。在需求分析过程中，要准确的定义系统的目标，把系统的每一个功能细节都尽可能地考虑周到，回答系统必须“做什么”的问题，并要考虑系统的性能。需求分析关系到软件系统开发的成败，是决定软件产品质量的关键。常见的需求分析方法主要分为三种：面向对象的分析方法、面向问题的分析方法和结构化的分析方法。

本系统采用了面向对象的分析方法，在需求分析过程中，将系统分为小的模块，确定业务逻辑，用UML建模方法，可视化的描述系统的功能。

#### 前端架构

小程序整体架构图如下所示：

![](https://github.com/early-month-subsidy/dashboard/blob/gh-pages/assets/images/System-architecture-diagram.png?raw=true)

小程序分为两个主要部分独立运行：view模块和service模块。view模块负责UI显示，它由wxml和wxss转换后的代码以及微信提供的相关辅助模块组成。一个view模块对应一个webview组件，也就是我们常规理解的一个页面，小程序支持多个view同时存在，view模块通过JSBridge对象来跟后台通信。

Service模块负责应用的 后台逻辑，它由小程序模块负责应用的 后台逻辑，它由小程序js代码以及微信提供的相 关辅助模块组成。一个 小程序应用只有service进程，它同样也是一个页面 进程，它同样也是一个页面 （至少在开发者工具内如此，上线后可能运行于 （至少在开发者工具内如此，上线后可能运行于 WeixinJSCore之中），它与 之中），它与 之中），它与 view模块不同的是， 它在程序生命周期内后台运行service模块通过与 view模块实现不同但接口格式一样的 JSBridge对象跟后台通信。
交互通过 JSBridge进行，当用户操作触发了事件通过 进行，当用户操作触发了事件通过 进行，当用户操作触发了事件通过 进行，当用户操作触发了事件通过 JSBridge通知逻 辑层，逻执行对应并把数据通过 JSBridge传递给视图层，执行 传递给视图层，执行 相应的操作。 

#### 微信小程序开发框架

微信小程序的框架 采用了 MVC开发思想，包括了逻辑层、视图和基础。 开发思想，包括了逻辑层、视图和基础。 开发思想，包括了逻辑层、视图和基础。 开发思想，包括了逻辑层、视图和基础。 小程序开 发框架的目标是通过尽可能简单、高效方式让者以在微信中小程序开 发框架的目标是通过尽可能简单、高效方式让者以在微信中发具有原生 APP体验的服务。框架提供了自己视图层描述语言 WXML和 WXSS，以及基于 JavaScript的逻辑层框架，并在视图与之间提供了数 据传输和时间系统，让开发者可以方便的聚焦于数逻辑上。
一个小程序的主体部分要由 3个全局文件组成， 必须放在项目的根录中个全局文件组成， 必须放在项目的根录中这三个全局文件分别是小程序公共样式表 app.wxss、小程序公共设置 、小程序公共设置 app.json和 小程序逻辑 app.js，它们 对所有的页面都是有效的。

#### 自己的一些感受

由于毕设是写了一个小程序的，所以现在写起来比较顺手，更重要的是，相对于Android Studio的安装，微信开发者工具实在是太简单了。微信小程序的登录相比以前改了一些改变，现在需要调用接口获取登录凭证（code)，然后后台通过凭证进而换取用户登录态信息，包括用户的唯一标识及本次登录的会话密钥等。还有后台lizijie同学完成的很好，提供了详细完整的API，前端后台交互很方便。
