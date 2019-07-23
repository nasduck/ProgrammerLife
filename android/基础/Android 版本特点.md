## 简述 Android 最近版本的特点

* [官网各版本特点](https://developer.android.google.cn/about/versions)

### Android 9 Pie API 28

* 利用 Wi-Fi RTT 进行室内定位. 例如楼内导航、基于精细位置的服务, 如无歧义语音控制（例如，“打开这盏灯”）, 以及基于位置的信息（如 “此产品是否有特别优惠？”）.
* 显示屏缺口支持即支持最新的全面屏, 其中包含为摄像头和扬声器预留空间的屏幕缺口.
* Android 9 引入了多个通知增强功能.
	* 进一步提升短信体验. Android 7 API 24 添加了一个操作以回复短信或直接从通知中输入其他文本. 9 进一步对其优化.
	* Android 9 简化了通知渠道的设置. Android 8 引入了通知渠道, 允许用户为要显示的每种通知类型创建可由用户自定义的渠道. 
* 多摄像头支持和摄像头更新
* 引入了 `ImageDecoder` 类取代 `BitmapFactory`.
* 动画. 引入 `AnimatedImageDrawable` 类，用于绘制和显示 GIF 和 WebP 动画图像.
* 新增 `JobScheduler` 来使用运营商提供的网络状态信号来改善与网络有关的作业处理.
* Android 8.1 API 27 中引入了 Neural Networks API 以加快 Android 设备上机器学习的速度. Android 9 扩展和改进了该 API.
* 自动填充框架. 进一步增强用户填写表单时的体验.
* 安全增强功能
	* Android Protected Confirmation
	* 统一生物识别身份验证对话框
	* 新增了与备份和还原有关的功能和开发者选项

其他新增功能以及更详细信息参考 [Android 9 Pie 新功能](https://developer.android.google.cn/about/versions/pie/android-9.0).

