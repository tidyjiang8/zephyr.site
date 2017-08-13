title: Zephyr OS 重磅推出1.8版本，源代码迁往GitHub
date: 2017-07-15 19:25:11
---

专为资源受限设备开发的 Zephyr 物联网操作系统宣布推出最新的 **1.8 版本**，对比上一版本，v1.8 的主要更新包括以下几点：
- Tickless 内核
- BT 5.0 功能
- 生态系统：支持通过第三方工具 Tracing 和 Debugging
- 改进的 Build 和 Debug
- 第三方编译器支持
- Xtensa GCC 支持
- 改进的 Build on Mac / Windows
- MMU / MPU： 初步支持（WIP）
- 扩展设备支持

这次发布是开源项目研发的一个重要里程碑： **将主要的源代码迁移到 GitHub ，从而进一步促进社区贡献和协作** 。

<!--more-->

![](github.jpg)

通过实施这一改变，开发者和贡献者可以通过提交 Pull 请求进行修改和添加，简化了审查和验收流程。随着过渡工作完成，300 多个 Pull 请求已经合并到 Zephyr 源代码中，Zephyr 项目欢迎更多代码或者文档贡献到代码库中。
除了在 Gitub 上托管外， Zephyr 资源可以轻松地在 Microsoft Windows 上构建：从 MinGW 向 MSYS2 的过渡允许用户轻松地在该平台上进行编译，不用担心之前在 Windows 构建环境中出现的稳定性问题。

此外，Windows 完全支持目前需要 Device Tree 支持的目标平台，从而可以采用微软操作系统来使用、开发，并贡献到 Zephyr 项目。

但是核心的实时操作系统自上次发布以来也看到了大量改变。**新的 tickless 内核优化推出，在电源管理中引入了一个“race to idle”方法，允许内核不中断地休眠，直到需要系统关注的事件唤醒它，而不需要定期的基于 tick 的中断**。另外，可以在某些平台支持和启用内存保护单元 (MPU)，这进一步加强了 Zephyr 项目对安全的承诺, 这也是项目理念的基本宗旨之一。不同执行代码之间的内存保护可以防止干扰甚至恶意篡改，而这只是个开始，Zephyr 会不断努力在后续版本中加强内核及子系统。
 
如今网络子系统配有一个 HTTP 客户端和服务器库，这允许嵌入式系统使用最流行的网络协议，并且不需要第三方软件，再加上最新的网络线程模型优化（由新内核的轮询API支持）和基于分组的接口进一步增强了 Zephyr 的内置原生IP堆栈，实现比以往更强大的 IoT 应用程序和使用案例。
 
最后，**蓝牙子系统已经从最近推出的蓝牙 5 规范中获得新的和令人兴奋的功能的支持**。Nordic 半导体公司某些 IC 运行 Zephyr 操作系统，现在能够超越蓝牙低功耗，以 2Mbit/s PHY 的速度进行数据传输，超过1.3 Mbit / s 的应用吞吐量，并且可以使用 nRF52 系列微控制器最新的 nRF52840 的编码PHY功能实现长距离通信。这只是迈向全面支持蓝牙 5 的第一步，这将继续到下版本，一个带有标志性的功能推出：广播协议扩展。
 
衷心地感谢所有对社区做出贡献的人们，新版本的发布离不开你们的贡献。欢迎开发者下载并使用 Zephyr OS 1.8，同时欢迎将意见和建议反馈到社区。

开发者可以通过点击阅读原文下载 Zephyr OS 1.8，或者进入 Zephyr 官网下载。