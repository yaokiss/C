## Mecanim动画系统简介

Mecanim具有以下特征:

* Mecanim动画系统是通过Avatar这个代理来实现设置角色动画中的骨架和蒙皮的。

* 开发者可以利用角色动画的重定向功能（Retargeting），将其他的任意动画动作绑定到开发者所指定的任何角色模型上，使得被绑定的角色也具有指定的动画功能，从而实现动画动作的可重复利用，极大提高游戏的开发效率。

即：Avatar可以识别角色中的骨骼结构、包含的动画，并通过Retargeting操作应用的其他的模型中。

* 在处理人类角色动画时，开发者可以使用动画状态机来处理各个不同动画之间的过渡和各种逻辑。

* 可以通过图形界面的方式很方便的来实现，而不必用脚本去一点点实现一些逻辑操作。

* 我们还可以通过身体遮罩的方法来处理和改变角色身体上不同部位的一些动画行为，而不必修改动画本身资源。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415210555.jpg)

## 如何应用Mecanim动画系统？

当将一个人物模型文件（*.fbx或*.obj)导入到Unity后，选中人物模型，在Inspector面板中选择Rig标签。如图 所示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415212541.jpg)

其中，Animation Type（动画类型）属性分4种类型供其选择：

* None（无动画类型）
* Legacy（老动画类型）
* Generic（一般的，通常的动画类型）
* Humanoid（人类的动画类型）
请选择Humanoid并点击Apply。Mecanim会尝试匹配已有的骨骼结构和Avatar的骨骼结构。大多数情况，它通过分析刚体的骨骼结构自动匹配。

如果匹配成功，你会在Configure…菜单旁边看到一个复选框（如下图）。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415212919.jpg)

成功匹配的同时，会添加一个Avatar子资源到FBX资源，您在project视图里面可以看到它。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415213046.jpg)

左图：不带Avatar子资源的模型 右图：带Avatar子资源的模型.

如果Mecanim没能创建Avatar，您会在Configure按钮旁边看到一个十字叉，不会添加Avatar子资源。此时，你需要手动配置avatar。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/noavatar.png)

## 配置Avatar

Avatar是Mecanim的一个如此重要方面，它需要被配置地符合你的模型。因此不论自动Avatar创建失败或者成功，你都需要进入Avatar配置模式来确保你的Avatar是有效并且合适地配置了。你的角色骨骼匹配Mecanim的预定义骨骼结构并且模型是T字形姿势是非常重要的。

如果自动Avatar创建失败，你将会看到一个叉号出现在Configure按钮旁边。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415213616.jpg)

如果配置成功，将会看到Configure…按钮旁边出现一个对号。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415213736.jpg)

在这里，成功简仅仅意味着需要的骨骼被匹配上了，但是为了获得更好的结果，你可能会想也匹配上可选的骨骼以及让模型进入一种合适的T字姿势。

当你进入Configure…按钮，编辑器将会问你是否保存场景。之后进入Configure模式，场景视图用来单独显示指定模型的骨骼，肌肉和动画信息，不显示场景的其他部分。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415213917.jpg)

一旦你保存了场景，你就会看到一个带有骨骼映射的新Avatar配置检视器

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415214009.jpg)

检视器显示哪些骨骼是需要的还有哪些骨骼是可选的-可选的骨骼的运动可以自动用插值计算出来。为了让Mecanim产生有效的匹配，你的骨架需要至少含有必须的骨骼在适当的位置。为了提高查找匹配Avatar的机会，可以使用反映身体部位的名称命名你的骨骼（像“LeftArm”“RightForearm”这样的名称都是合适的）。

如果模型没有产生一个有效的匹配，你可以手动按照类似Mecanim内部的处理方式做一下：

1. Sample Bind-pose
采样绑定姿势（尝试让模型更接近它建模时候的姿势，一个合理的最初姿势）

2. Automap
自动映射（从最初的姿势创建一个骨骼映射）

3. Enforce T-pose 强制T字姿态
强制让模型更接近T字姿态，这是Mecanim使用的默认姿势。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415214219.jpg)

如果自动映射（Mapping->Automap）完全或者部分失败，你可以通过从场景或者体系结构视图拖拽它们来赋值到骨骼。如果Mecanim认为骨骼合适，它会用绿色在Avatar检视器中显示，否则会以红色显示。

最后如果骨骼被正确赋予了，但是角色不是在正确的姿势，你将会看到消息“Character not in T-Pose（角色不是在T字姿态）”。你可以尝试Enforce T-pose(强制T字姿态)或者旋转余下的骨骼到T字姿态。


人体模板（human template）

你可以用“人体模板文件”(扩展名*.ht)的形式保存骨骼到你Avatar骨架的映射到到磁盘上，你可以在任意角色上重用这个映射。这非常有用，比如，如果你的动画使用一致布局和命名约定到所有的骨架上但是Mecanim不知道如何解释它。你可以为模型载入.ht文件，这样手动重映射只需要做一次。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%9F%BA%E7%A1%80/images/20170415214348.jpg)



## Avatar系统

利用Avatar系统，我们可以通过对骨胳操控实现动画的重利用效果，这也就是Mecanim系统中的动画重定向功能。

## Avatar工作原理

对于人类角色来说，都包含着相同或者类似的骨骼。而Avatar，可以对角色中包含的骨骼结构或者角色模型进行分析与识别，并与Mecanim中已有的标准人类骨骼进行对比，并进行标示。它是一个接口，通过它可以被Mecanim系统所识别，成为一种可被Mecanim系统所识别的通用的骨骼结构，并把一副骨骼的动作指定应用到另一副骨骼中，即实现Retargeting重定向。

##　创建并配置Avatar

选中人物模型，在Inspector面板中选择Rig（装备）标签。如图 所示。
其中，Animation Type（动画类型）属性分4种类型供其选择。
分别是

* None（无动画类型）
* Legacy（老动画类型）
* Generic（一般的，通常的动画类型）
* Humanoid（人类的动画类型）。
如果要应用Avatar，则需要选择最后一个类型，即Humanoid类型选项。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_9.png)

选择Humanoid类型之后，则可以看到Avatar Definition（Avatar定义）属性选项。分为Create From This Model（为此模型创建Avatar）、Copy From Other Avatar（复制其它的Avatar）两种选项。选择第一项并Apply确定后，则会自动创建Avatar。如果创建成功，则会在下面的Configure…（配置）按钮前有一个对勾，表示Avatar被创建成功


![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_10.png)

点击Configure按钮，我们可以图形化手动配置Avatar。Mecanim要利用Scene场景视图来显示骨骼图形界面，所以当点击Configure按钮后，Unity会提醒保存当前场景。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_11.png)

在Inspector面板中，Avatar以图形方式绘制显示在Mapping（绘图）映射图表标签中。其中圆形图标代表了人体骨骼的节点。通过点击某一个圆形图标，可以选中不同部位的骨骼。而圆形图标分为实线和虚线两种。虚线圆表示为Optional Bone（可选的骨骼），而实线圆则表示为Avatar必须要设置的骨骼。
在Mapping绘图标签中，有4个按钮分别代表了人物骨骼的4个不同的细节部位。Body（身体）、Head（头部）、Left Hand（左手）、Right Hand（右手）。

当骨骼匹配都正确时，则图案都为绿色，只有在骨骼匹配错误时，才会在错误的对应点显示为红色，并自动弹出一些错误提示。如图 所示。这时开发者可以通过手动方式重新为其添加正确的骨骼映射匹配。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_12.png)

除了手动调整骨骼Avatar的骨骼匹配，Unity的Mecanim还为我们提供了一些自动的匹配方式：
* 选择Pose（姿势）属性下拉菜单中的Sample Bind-Pose（取样姿势绑定）选项。如图 所示。
* 选择Mapping（映射）属性下拉菜单中的Automap（自动映射）选项。如图 所示。
* 选择Pose（姿势）属性下拉菜单中的Enforce T-Pose（强制T-Pose）选项。如图 所示。
* （可选）选择Mapping（映射）属性下拉菜单中的Save（保存）选项，对新的骨骼映射进行保存。这样可以为以后其它的人物资源配置应用骨骼映射了。再应用的时候可以选择Mapping（映射）属性下拉菜单中的Load（加载）骨骼映射选项。
* 5、最后，不要忘记点击Apply应用一下。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_13.png)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_14.png)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_15.png)

## Avatar的Retargeting重定向

只有在通过Avatar处理过的骨骼（且必须为人类的骨骼）才能再通过Retargeting重定向，即经过Avatar处理过的骨骼具有相同或类似的骨骼结构，这样可以使骨骼（或者说不同的动画片段）在不同的角色中重用或者互用。即A人物的骨骼或者说动画片段可以应用在B人物模型身上（甚至B人物身上可以没有任何动画片段或者有自己的动画片段都没关系）使之具有A人物模型身上的动画行为，反之亦可。
所以，当骨骼经过Avatar处理后，只需要对每个模型添加一个Animator Controller（动画控制器），则在播放游戏时，不同的模型则具有了相同的动画。如图 所示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_16.png)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_17.png)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_18.png)

## Avatar肌肉设定

除了正确匹配骨骼位置，还可以通过Muscles（肌肉）属性来微调骨骼的运动范围，从而使骨骼动画更合理协调，避免在骨骼动画中出现身体叠加或者失真的现象。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Avatar%E7%B3%BB%E7%BB%9F/images/20170419_19.png)

如图 所示，在Muscle Group Preview（肌肉组合预览）中，可以观察一系列多个不同骨骼组合的共同运动效果。可以点击Reset All（重置所有）按钮来恢复成默认的预览。
而在Per-Muscle Settings（每一个肌肉的设置）中，可以调整身体不同部位的单独骨骼肌肉拉伸范围，并对其微调设置。如果我们想恢复默认值，则可以点击最下面的Muscles下拉菜单，选择Reset（重置）选项来恢复。也可以在点击Apply应用之前，点击最下面的Revert（重置）按钮恢复。
最后一组设置为Additional Settings（附加设置）。可以微调骨骼的扭曲效果。
最后选择Apply应用，并选择Done（完成）按钮来保存微调设置并回到游戏场景中。



## 动画切割案例


选中角色资源，在Inspector面板中会显示Import Settings（输入设置）。

在Animations动画标签中可以看到Clips动画片段。Clips中就只有一个动画片段，叫Take 001。其动画帧数范围为：0-330帧。播放下面预览窗口的播放按钮可以看到整个动画里包含2个动作行为。

因为动画片段的原始帧范围为1-330，不是0-330。则下面会显示“The clip range is outside of the range of the source take.”，表示片段的范围已经超出原始资源片段的帧范围。需要单击Clamp Range（强制实行范围）按钮来剪切。

根据需求单击加号来添加动画片段，并确定2个动画片段的帧范围，并命名对应的动画片段。idle 为：1-240 ，walk为： 300-330。


![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%8A%A8%E7%94%BB%E5%88%86%E5%89%B2%E4%B8%8E%E8%AE%BE%E7%BD%AE/images/cutanim.png)

## 动画片片段

在Unity的Mecanim系统中可以对不同的动画片段进行动画融合和动画过渡等操作，这就要求需要有循环质量比较高的动画片段来保障动画的效果。Mecanim提供了一些工具和属性，对于动画片段的循环进行监测和优化调整。

在Project面板中选中一个动画模型，在Inspector面板中的Animations标签下，可以选中一个动画片段。则在下面显示了针对此动画片段所对应的动画循环的属性监测。在此属性编辑器中，提供了一些显示，来描述其动画片段的各种循环质量的参数。如图所示。

分别有4个属性设置：

Loop Time，勾选这个选项之后，如果Animator处于播放这个动画状态时，在播放完第一遍这个动画片段之后，会自动循环从起始帧再次开始播放动画，如此循环往复。
如果我们不勾选这个选项，例如Animator一直处于播放这个动画的状态，那么动画会定格在动画的结束帧，直到我们通过Animator切换这个Animator状态机的状态，切换到其他的动画

Loop Pose用于控制动画循环播放时，从结束帧切换到起始帧时，动画的动作可以无缝的衔接上，

Cycle Offset就是用于控制循环的时候起始帧偏移用的

* Root Transform Rotation 根旋转变换
* Root Transform Position (Y) 根位置变换（Y）根节点位移信息（Y轴）
* Root Transform Position (XZ) 根位置变换(XZ) 根节点位移信息（水平面，XZ轴）

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%8A%A8%E7%94%BB%E5%88%86%E5%89%B2%E4%B8%8E%E8%AE%BE%E7%BD%AE/images/20170415220437.jpg)

（注：Original是角色原始位置，Center of Mass为角色重心在y轴的投影位置）

以上4个属性分别匹配的非常好时（即动画的起始帧与结束帧比较吻合），右面对应的等会呈现绿色。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%8A%A8%E7%94%BB%E5%88%86%E5%89%B2%E4%B8%8E%E8%AE%BE%E7%BD%AE/images/jdfw.gif)

## [案例1]Root Transform Position (Y)

根位置变换（Y）根节点位移信息（Y轴）应用

如图 所示，在动画预览中，我们看到模型与地面保持有一点空间距离，这样会导致任务在游戏运行时浮空在游戏场景中。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%8A%A8%E7%94%BB%E5%88%86%E5%89%B2%E4%B8%8E%E8%AE%BE%E7%BD%AE/images/eb8de5a5-1bc3-4f72-aba2-222e4befc472.jpg)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%8A%A8%E7%94%BB%E5%88%86%E5%89%B2%E4%B8%8E%E8%AE%BE%E7%BD%AE/images/9a60e9da05d6.jpg)

我们可以调节Root Transform Position (Y) 根位置变换（Y）属性，勾选Bake Into Pose（烘焙到姿势中）选项，并调整Offset（位移）数据，使其贴服在地面上


## [案例2]Root Transform Position (XZ)

根位置变换(XZ) 根节点位移信息（水平面，XZ轴）
如图 所示。在x轴方向上有一定的运动量。我们调整Offset偏移量，使Average Velocity（平均速度）属性在x轴的运动量为0。这样就可以保证人物模型沿着x轴直线跑动而不产生角度偏移了。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animator%E5%8A%A8%E7%94%BB%E5%88%86%E5%89%B2%E4%B8%8E%E8%AE%BE%E7%BD%AE/images/a31867b44044.jpg)
























