## Root Motion设置

### Root Motion根运动

### Root Motion根运动

Root Motion根运动是一个非常重要的概念。它的原理是：当身体发生了变换，从而引发身体的重心发生改变。即改变了重心或者说身体的方向。这样在地面上则产生了方向上的投影。角色身体的上半身也下半身相对于角色T-pose进行平均计算而产生一个方向矢量。身体变换和方向则在每一帧中都会把变化计算出来，并都存储到动画片段 (Animation Clip) 中。最后施加到游戏对象上。当我们在Inspector面板中勾选上Animator组件中的Apply Root Motion（应用根运动）属性，则会使其产生带方向的移动，而不必在脚本中用Transform方法使其产生位移了。如图 所示。如果不够选此选项，则只会播放动画，而不会产生位置偏移。
即Unity的Mecanim中，利用角色动画片段中的Root Motion来控制角色在场景中的运动，真正的使角色动画实现了角色运动的驱动。这点对于老版本的动画来说是一个非常大非常方便的改变与提升。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8720.png)

## 动画组件与动画控制器

Animator动画组件

Animator组件是控制角色模型中的动画行为的组件，或者说是人物模型与动画之间的一个连接。如图 所示。
Animator组件的属性：
* 1、Controller：指定动画控制器资源。动画控制器资源包含了动画的各种逻辑，从而控制角色的运动行为。
* 2、Avatar：指定了Avatar资源，可以使用角色通用的骨骼设置。
* 3、Apply Root Motion：使用Root Motion选项。（上节已做详细介绍）。
* 4.Update Mode：更新模式：Normal表示使用Update进行更新，Animate Physics表示使用FixUpdate进行更新（一般用在和物体有交互的情况下），Unscale Time表示无视timeScale进行更新（一般用在UI动画中）。
* 5.Culling Mode：剔除模式(优化使用)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8732.png)

## Animator Controller动画控制器

Animator动画控制器可以设置角色的动画执行逻辑以及动画之间的过渡方式。创建动画控制器非常方便，在Project面板中->Create->Animator Controller。如图 所示

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8733.png)

创建好动画控制器后，双击，则会打开Animator Controller视窗。如图 所示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8734.png)

我们可以在Animator Controller动画控制器界面中通过点击鼠标右键来添加各种状态机，包括指定默认的状态机、Any State（任意状态）、Blend Tree（混合树状态）、New StateMachine（新状态机）等。我们会在后面的章节做详尽的讲解。

在动画控制器左下角是Parameters（参数）[pə’ræmətɚ]。可以创建4种类型的参数。创建后，可以对参数进行命名或设置其初始值。而动画状态机都是要配合开发者设置的参数来控制其动画之逻辑。


## 动画状态机及动画过渡

简单的讲，动画状态机可以使一个动画状态过渡到另一个动画状态。通过设置状态之间的过渡，可以非常简单的定义动画之间的逻辑，从而减少繁杂的代码的处理，使动画间的逻辑处理更加的简单、高效。而且进行更新时，也非常的快速。
在创建动画状态机时，每一个动画片段可以看做为一个动画状态机的节点。在Animator窗口面板->单击鼠标右键->Create State->Empty，即可创建一个空的动画状态机。如图 所示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8735.png)

状态机的属性介绍：如图 所示。
* 1、Speed：指定动画的播放速度。默认为1。可以根据需求加速或者放缓动画的播放速度。
* 2、Motion：指定此动画状态所使用的动画片段。
* 3、Foot IK：在此状态中是否考虑或计算动画中的Foot IK。
* 4、Mirror：产生用动画对应的镜像动画效果。比如动画片段是向左转的动画，通过勾选镜像参数，则会产生向右转的镜像动画。
* 5、Transitions：显示从此节点可以过渡到其它哪些的节点。如图 所示，可以从Base layer层的idle动画可以过渡到Base Layer层的walk动画。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8736.png)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8737.png)

第一个创建的动画状态机为默认的状态，游戏运行时会先执行此状态的动画，而默认状态为黄色。我们也可以手动指定默认的状态。只要选中要指定的状态->鼠标右键->Set As Default即可。如图 所示。
此时，在Inspector面板中的Motion（动作）属性中，可以拖放进来要播放的对应的动画片段。当然，方便起见，也可以通过拖拽动画片段直接到Animator窗口面板中，则可直接创建一个对应的动画状态。如图 所示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8738.png)

有了不同的动画片形成不同的动画状态，使它们之间的过渡，才能把不同的状态关联起来。我们选中一个状态->鼠标右键->Make Transition即可完成动画间的过渡。如图 所示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8739.png)

从一个动画状态机过渡到另一个动画状态，需要一定的要求或者限制。我们可以通过设置左下角的Parameters（参数）属性来完成。

一个Animator动画状态机的窗口视图打开后，一般会有一个绿色的动画状态，Any State（任意动画状态）。我们可以理解此为不确认的动画状态，或者理解为是任意的动画状态。也就是说，当它与某个动画状态创建过渡后，则说明任何的动画状态只要满足条件后都可以过渡到此动画状态中。比如，Any State过渡到dead死亡状态，则说明任意动画状态只要满足游戏人物死亡的条件时，都可以过渡到dead动画状态上。
控制动画状态过渡实例
* 1、创建Animator状态机，并添加idle和walk两个动画状态。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8740.png)

2、添加walk参数。并指定过渡。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/14_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_AnimatorController/img/%E5%9B%BE%E7%89%8741.png)


3、脚本

```C#
using UnityEngine;
using System.Collections;

public class AnimatorController : MonoBehaviour {

    private Animator anim;//声明Animator动画组件
    void Start()
    {
        anim = this.gameObject.GetComponent<Animator>();//获取Animator组件
    }

    void Update()
    {
        if (anim)//如果Animator组件是存在的
        {
            //获取当前层，0为基础层
            AnimatorStateInfo currentStateInfo = anim.GetCurrentAnimatorStateInfo(0);

            //如果Base Layer层的idle状态存在
            if (currentStateInfo.IsName("Base Layer.idle"))//等价于:stateInfo.nameHash == Animator.StringToHash("Base Layer.idle")
            {
                //当点击键盘A键的时候	，设置walk状态为真(由idle状态过渡到run状态)
                if (Input.GetKeyDown(KeyCode.A)) anim.SetBool("walk", true);
            }

            if (currentStateInfo.IsName("Base Layer.walk"))
            {
                if (Input.GetKeyDown(KeyCode.B)) anim.SetBool("walk", false);
            }
        }
    }
}
```







































