## 目录

* [简述 Android 的系统架构](#简述Android的系统架构)
  * [架构图](#架构图)
  * [Linux_内核](#Linux内核)
  * [硬件抽象层](#硬件抽象层)
  * [Android Runtime](#AndroidRuntime)
  * [原生 C/C++ 库](#原生C/C++库)
  * [Java API 框架](#JavaAPI框架)
  * [系统应用](#系统应用)
* [参考](#参考)  

## 简述Android的系统架构

Android 系统采用**基于 Linux 的分层架构**.

### 架构图

![Android 系统架构](https://github.com/nasduck/ProgrammerLife/blob/master/android/%E6%9E%B6%E6%9E%84/img/android-system-arch.png)

从下往上说:

#### Linux内核

最底层是 Linux 内核, 也是 Android 平台的基础. 为安卓设备的各种硬件提供了底层的驱动, 如显示驱动, 照相机驱动, 电源管理等.

#### 硬件抽象层

再往上是硬件抽象层 Hardware Abstraction Layer - HAL, 它负责提供标准接口, 向更高级别的 Java API 框架显示设备硬件功能. HAL 包含多个库模块, 其中每个模块都为特定类型的硬件组件实现一个接口, 例如相机或蓝牙模块. 当框架 API 要求访问设备硬件时, Android 系统将为该硬件组件加载库模块.

#### AndroidRuntime

对于运行 Android 5.0（API 级别 21）或更高版本的设备, 每个应用都在其自己的进程中运行，并且有其自己的 Android Runtime (ART) 实例. ART 编写为通过执行 DEX 文件在低内存设备上运行多个虚拟机，DEX 文件是一种专为 Android 设计的字节码格式，经过优化，使用的内存很少。编译工具链（例如 Jack）**将 Java 源代码编译为 DEX 字节码**, 使其可在 Android 平台上运行.

ART 的部分主要功能包括：

* 预先 (AOT) 和即时 (JIT) 编译
* 优化的垃圾回收 (GC)
* 更好的调试支持, 包括专用采样分析器、详细的诊断异常和崩溃报告, 并且能够设置监视点以监控特定字段

在 Android 版本 5.0（API 级别 21）之前, Dalvik 是 Android Runtime。

Android 还包含一套核心运行时库, 可提供 Java API 框架使用的 Java 编程语言大部分功能，包括一些 Java 8 语言功能.

#### 原生C/C++库

许多核心 Android 系统组件和服务（例如 ART 和 HAL）构建自原生代码, 需要以 C/C++ 编写的原生库. Android 平台提供 Java 框架 API 以向应用显示其中部分原生库的功能. 例如, 可以通过 Android 框架的 Java OpenGL API 访问 OpenGL ES，以支持在应用中绘制和操作 2D 和 3D 图形.

如果开发的是需要 C 或 C++ 代码的应用, 可以使用 Android NDK 直接从原生代码访问某些原生平台库.

#### JavaAPI框架

提供应用程序构建时用到的各种 API. 如视图(View), Content Provider, 以及各种管理器, 比如活动管理器, 通知管理器等.

开发者主要也是通过这些 API 来开发自己的应用程序.

#### 系统应用

是核心应用程序的集合, 所有安装在手机上的应用程序都属于这一层, 如系统自带的电子邮件、短信、日历、互联网浏览和联系人等核心应用. 

## 参考

* [平台架构](https://developer.android.google.cn/guide/platform/)
