## AnimationEvent的添加方法

选中具有Animation动画组件的模型，并拖动到场景中。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/6eec9eb5-700e-4901-9a8c-fecf0c967dce.png)

模型具有两个动作，分别是pose 和 wait
按快捷键Ctrl+6 打开动画编辑器,通过顶部的图标来可以为选中的帧添加一个事件。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/96b24b2b-c2c7-413c-9430-a194ef8fee2a.png)

添加出事件后，在关键帧顶部，会显示出一白色的小块，说明此处已经添加了事件，并且会弹出下面的一个弹窗,此时还没有任何可以调用的方法供选择。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/037cb752-94f5-4e5a-90ca-f969a845be37.png)

我们需要新建一个脚本AnimationEventDemo.cs，并挂载到角色身上，并在脚本中声明public类型的方法TestFun1();

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/8c2eecff-9ecc-4c81-bc2d-df0b5daab610.png)

代码编写完成后，再次返回动画编辑器，双击刚刚添加的事件，此时在当前的弹窗中，已经把我们声明的TestFun1方法列了出来，我们选中此方法。返回Unity进行播放测试。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/f7e43f17-7077-41f0-932d-324c84a3ca5b.png)

返回Unity进行播放测试，动画进行播放，并且在Console窗体已经输出了相应的信息

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/ceec8f5a-dbaa-4e6d-9eea-d1b7e8d919d1.png)

2.通过代码实现动画事件的添加
我们给动画添加事件，要先通过Animation组件的GetClip(clipName)方法,获取要添加事件的动画片段(AnimationClip).

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/f972e57f-3b59-4bc8-9a3e-9462ad3aeef4.png)

同样可以调用到方法TestFun2

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation%E4%BA%8B%E4%BB%B6/images/186a67d9-91a5-46a0-9621-1ffd7e9c4bbd.png)
