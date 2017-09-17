# OpenCV--机器人计算机视觉
基于计算机视觉智能车寻路系统
简介:
视觉辅助机器人它可以前往相机视野范围内任意一个你希望它去的点。
在我们的方案中，在天花板上会有一个相机附着，一旦你从机器人那获得视频流并点击视野内的任意一个地方，那么这个机器人就会去那里。
这个操作系统要求移动机器人能够与视觉系统进行通信。
视觉系统能够检测或者识别出机器人并计算出机器人的位置和方向。这个视觉系统也让我们可以点击视野中的任意一点，并且能够计算机器人到这点的路径以及机器人如何移动到这一点。
系统总览：
上位机（PC） 摄像头Arduino（主） NRF无线模块    Arduino（从） NRF无线模块  小车循迹系统   视觉机器人
数据采集：
我们使用场景的视频流，在视野内安装一个摄像头当作采集器，通过机器人上面的红蓝的圆圈检测机器人位置并计算其方向
预处理阶段：
首先出去表面小细节，调整图像输入以减小图像大小和处理时间，同时保持能够正常从图像中提取有效的信息
处理图像：
第一步，检测图像中的红蓝圆圈。提取到的图像信息使用颜色滤波器来处理红蓝颜色掩码，接着使用Blob分析来检测圆圈并提取有效的特征。
第二步，计算机器人的方向和到达目的地的路径。主控制器
从控制器指令无线传输：
通过无线对机器人发送指令，在这个系统中，我们采用两个NRF24L01模块，第一个模块连接到机器人控制器，第二个模块连接到视觉控制器
循迹控制系统：
无线模块接收到主控制器发送的行动指令，使用Arduino控制器配合L293D电机驱动模块，让两个电机按照指令行动，从而到达目的地
机器人构建动力系统：
机器人控制系统设计相对简单，由一个差动驱动的简化版操控。
差动驱动简单概括为在两个轮子上存在一个相对速度差异，这将导致机器人的方向发生变化，同时可以通过改变轮子的旋转速度来让机器人走弯曲的路径。
力学系统：
我们把齿轮电动机附着在亚克力板靠前的位置，各种模块放在盒子上面。机器人最上面加上纯色覆盖以增大红蓝色圆圈的对比度。
电子电路部分：
使用两个单独的Arduino控制板，一个主控制视觉系统，一个从控制机器人。选用NRF24L01模块做无线通信，使用一个四倍H桥驱动——L293D。
机器人/接收器图纸：
使用USB电缆连接到OpenCV平台，不需要外部电源供电NRF24L01无线模块Arduino主控制器
发射器图纸;
电机驱动电机电池NRF24L01系统采用两个电源供电，将电动机电源和Arduino电源分开。当电动机处于高负载状态运行时，可能会导致Arduino供电不足，因此选择两个电源来消除这种影响。Arduino和电动机采用9V独立供电
构建视觉应用程序         
我们使用第二块Arduino来与机器人上的Arduino进行通信，一个网络摄像头通过USB连接到笔记本电脑上。
视觉控制应用程序包括一个串口通信模块通过射频收发器来与机器人进行通信（可以使用标准蓝牙和低功耗蓝牙或者ZigBee），如果可以想在机器人和笔记本电脑之间直接建立连接而不走外部电路，低功耗蓝牙将是一个不错的选择。
这个视觉控制应用程序是用在Windows 10上的Visual Studio 2013创建OpenCV项目；
对于串口通信，我们使用Windows平台上的Arduino串口通信，非常易于实现和集成化。
这个应用程序选择以Blob分析为基础的处理技术，使用了开源的cvBlobsLib库。
应用场景:      
本系统为计算机视觉控制系统，具有友好人计交互界面，在工业和生活中均具有巨大的使用前景。
在普通生活中可以用于自动化远程控制家居系统
如果应用于工业机器人控制中，可以使得机器人操作在一定的视距内取得精准的定位。
同时，此平台兼容Windows   MacOS   Linux等多种操作系统,同时还能与安卓苹果等手机建立连接。
