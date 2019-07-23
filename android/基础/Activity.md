## 目录
 * [Acticity生命周期](Acticity生命周期)
 * [Activity生存周期](Activity生存周期)
 * [Activity生命周期调用顺序](Activity生命周期调用顺序)

## Acticity生命周期
### onCreate(Bundle savedInstanceState)
执行基本的应用程序启动逻辑，该逻辑在活动的整个生命周期中只应发生一次。
例如：加载布局、绑定数据、绑定事件
该方法接收的参数是活动先前保存状态的对象。

### onStart()
对用户可见，但是还无法与用户进行交互。
此方法是应用程序初始化维护UI的代码的位置。

### onRestart()
当当前Activity从不可见重新变为可见状态时调用。

### onResume()
应用程序与用户交互的状态。
任何与活动生命周期相关的生命周期感知组件都将收到该 ON_RESUME 事件。这是生命周期组件可以启用在组件可见且在前台时需要运行的任何功能的位置。

### onPause()
表示活动不再在前台（尽管如果用户处于多窗口模式，它仍然可见）。
这是生命周期组件可以停止在组件不在前台时不需要运行的任何功能的地方。
释放系统资源，处理传感器（如GPS），或在您的活动暂停且用户不需要时可能影响电池寿命的任何资源。
不使用 onPause()保存应用程序或用户数据，进行网络通话，或执行数据库事务。

### onStop()
活动不再对用户可见。
生命周期组件可以停止在组件在屏幕上不可见时不需要运行的任何功能的地方。
应用程序应释放或调整应用程序对用户不可见时不需要的资源。
对CPU密集型的关闭操作。例如，如果找不到更合适的时间将信息保存到数据库，则可以在此期间执行此操作。

### onDestroy()
在活动被销毁之前被调用。系统调用此回调因为：
活动正在结束（由于用户完全解雇活动或因活动 finish()被召唤）。
由于配置更改（例如设备旋转或多窗口模式），系统暂时销毁活动。

## Activity生存周期
### 完整生存期
Activity在onCreate()方法和onDestroy()方法之间所经历的周期。在onCreate()中进行初始化操作，在onDestroy()中进行进行销毁操作。

### 可见生存期
Activity在onStart()方法和onStop()方法之间所经历的周期。可以这两个方法中合理地管理对用户可见的资源，在onStart()中对资源进行加载，在onStop()中对资源进行释放。

### 前台生存期
Activity在onResume()方法和onPause()方法之间所经历的周期。活动总是处于运行状态，可与用户进行交互。

## Activity生命周期调用顺序
#### 一个Activity的启动：
回调顺序：onCreate -> onStart -> onResume

#### Activity显示状态下，按下home键：
回调顺序：onPause -> onStop

#### 从手机后台重新调出App：
回调顺序：onRestart -> onStart -> onResume

#### Activity A跳转到Activity B：
当Activity B是一个正常的Activity时：     
回调顺序：A_onPause -> B_onCreate -> B_onStart -> B_onResume -> A_onStop     
当Activity B是一个对话框形式或者透明的Activity形式的Activity时：    
回调顺序：A_onPause -> B_onCreate -> B_onStart -> B_onResume     

#### Activity B返回到Activity A：
当Activity B是一个正常的Activity时：    
回调顺序：B_onPause -> A_onRestart -> A_onStart  -> A_onResume -> B_onStop -> B_onDestroy     
当Activity B是一个对话框形式或者透明的Activity形式的Activity时：     
回调顺序：B_onPause -> A_onResume -> B_onStop -> B_onDestroy     

#### 横屏切换到竖屏的时候：
未设置android:configChanges时：但会调用onSaveInstanceState和onRestoreInstanceState来做数据暂存     
回调顺序：onPause -> onSaveInstanceState -> onStop -> onDestroy -> onCreate -> onStart -> onRestoreInstanceState -> onResume     
设置android:configChanges时：     
activity不会被销毁，会调用onConfigurationChanged     

#### 对话框出现在前台：
回调顺序：onPause （这个是不对的，在创建对话框的时候传入了对应activity的context）
