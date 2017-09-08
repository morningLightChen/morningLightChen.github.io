#AR开发-接触AR
##一、认识AR

首先让我们了解一下AR，VR以及MR的含义。

1、VR（Virtual Reality  虚拟现实），是近年来出现的高新技术。虚拟现实是利用电脑模拟产生一个三维空间的虚拟世界，提供视觉、听觉、触觉的感官模拟，让使用者如身临其境。

2、AR（Augmented Reality 增强现实）,它通过电脑技术，将虚拟的信息应用到真实世界，真实的环境和虚拟的物体实时地叠加到了同一个画面或空间同时存在。 之后的文章主要介绍的就是学习在iOS手机端上如何开发AR效果的app。

3、MR（Mix reality 混合现实）通过全息图，将现实环境与虚拟环境相互混合，也可以看成是VR与AR的混合。

##二、一个最最简单的AR项目
####项目准备
Xcode9可以直接创建AR项目，如下图选中项：

![](/Users/songchenguang/Desktop/ARProject.png)

这里语言用的是swift，content technology用的SceneKit

SceneKit 我理解的是 iOS中的一个3D引擎框架，代码中的一些类都是这个框架里面的。

此时,Xcode会自动为我们生成一段极其简洁的AR代码 代码如下：

设置场景

	@IBOutlet var sceneView: ARSCNView!//这个是AR场景类
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // Set the view's delegate
        sceneView.delegate = self //设置代理
        
        // Show statistics such as fps and timing information
        sceneView.showsStatistics = true//是否显示底部的fps
        
        // Create a new scene
        let scene = SCNScene(named: "art.scnassets/ship.scn")!//场景赋予一张图片
        
        // Set the scene to the view
        sceneView.scene = scene//给场景视图添加场景
    } 
AR场景跑起来
	
	override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        
        // Create a session configuration
        //创建一个追踪设备配置（ARWorldTrackingSessionConfiguration主要负责传感器追踪手机的移动和旋转）
        let configuration = ARWorldTrackingConfiguration()
		// 开始启动ARSession会话（启动AR）
        // Run the view's session
        sceneView.session.run(configuration)
    }
    
最简单的AR效果的demo就出来了
<img src="/Users/songchenguang/Desktop/IMG_0422.PNG" width="50%" height="50%" />
<img src="/Users/songchenguang/Desktop/IMG_0423.PNG" width="50%" height="50%" />

##三、介绍一下AR效果实现、ARKit相关
###基础技术视觉惯性测量计

ARKit 使用视觉惯性测量计 (Visual Inertial Odometry, VIO) 来精准追踪周围的世界。VIO将摄像头的传感器数据同 Core Motion 数据进行融合。这两种数据允许设备能够高精度地感测设备在房间内的动作，而且无需额外校准。
###	场景识别与光亮估量
借助 ARKit，iPhone 和 iPad 可以分析相机界main中所呈现的场景，并在房间当中寻找水平面。 ARKit 不仅可以检测诸如桌面和地板之类的水平面，还可以在较宵特征点 (feature points) 上追踪和放置对象。ARKit 还利用摄像头传感器来估算场景当中的可见光总亮度，并为虚拟对象添加符合环境照明量的光量。
### 高性能硬件与渲染优化
ARKit 运 在 Apple A9 和 A10 处 器上。这些处理器能够为 ARKit 提供突破性的性能，从而可以实现快速场景识别，并且还可以让您基于现实世界场景，来构建详细并引人注目的虚拟内容。 您可以   Metal、Scenekit 以及诸如 Unity、虚幻引擎之类的第三方工具，来对 ARKit 进行优化。

###ARKit的主要类别
#####1. ARSession类
 这是一个单例，是ARKit的核心类，用于控制设备摄像头，处理传感器数据，对捕捉的图像进行分析等。
  
#####2. ARSessionConfiguration类
跟踪设备方向的一个基本配置, 在运行时，需要指定AR运行的配置
#####3. ARWorldTrackingSessionConfiguration类
 配置跟踪设备的 向和位置,以及检测设备摄像头所看到的现实世界的表 
#####4. ARSCNView类
 用来增强相机通过 3D SceneKit 所捕捉到的内容并展示 AR 效果的一个 view
#####5. ARSKView类
 来增强相机通过 2D SpriteKit 所捕捉到的内容并展  AR 效果的一个 view
#####6. ARAnchor类
真实世界的位置和方向, 用于在一个AR场景中放置一个物体
#####7. ARPlaneAnchor类
在一个AR Session 会话中检测一个真实世界中平面的位置和方向的相关信息
#####8. ARHitTestResult类
在一个AR Session会话中通过检测相机视图中的一个点来获取真实世界中表面的相关信息
#####9. ARFrame类
捕获一个视频图像和位置追踪信息作为一个AR 会话的一部分。
#####10. ARCamera类 
在一个AR会话中摄像机的位置和成像特征信息为捕获视频帧
#####11. ARLightEstimate类
在一个AR会话中估计场景照明信息关联到一个捕获的视频帧
####下一篇[AR_全息太阳系](https://morninglightchen.github.io){:target="_blank"}
- List
