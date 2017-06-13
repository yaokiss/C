## 分离网格链接组件(Off-MeshLink)

案例

Off-MeshLink组件用于手动指定路径线路。可以实现跨越鸿沟或者往高处跳跃而上的效果。

1.创建场景。如图 所示。inv对象中有2个Cube，分别代表地板和大方块高墙。再创建2个Cube，分别命名为：start point和end point，分别为指定跳跃起点和指定跳跃终点位置点。使用胶囊体创建主角。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/15_%E5%AF%BC%E8%88%AA%E7%BD%91%E7%BB%9C%E5%AF%BB%E8%B7%AF_OffMeshLink/images/%E5%9B%BE%E7%89%8713.png)

2.把inv环境中的Cube物体设置为静态，并勾选OffMeshLink Generation选项。如图 所示

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/15_%E5%AF%BC%E8%88%AA%E7%BD%91%E7%BB%9C%E5%AF%BB%E8%B7%AF_OffMeshLink/images/%E5%9B%BE%E7%89%8714.png)

3.为start point添加Off Mesh Link组件。并把start point和end point拖放指定到Start和End属性中。如图 所示

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/15_%E5%AF%BC%E8%88%AA%E7%BD%91%E7%BB%9C%E5%AF%BB%E8%B7%AF_OffMeshLink/images/%E5%9B%BE%E7%89%8715.png)

4.为主角胶囊体添加Nav Mesh Agent组件。如图 所示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/15_%E5%AF%BC%E8%88%AA%E7%BD%91%E7%BB%9C%E5%AF%BB%E8%B7%AF_OffMeshLink/images/%E5%9B%BE%E7%89%8716.png)

5.Bake烘焙场景。注意调节Height、Drop Height、Jump Distance属性。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/15_%E5%AF%BC%E8%88%AA%E7%BD%91%E7%BB%9C%E5%AF%BB%E8%B7%AF_OffMeshLink/images/%E5%9B%BE%E7%89%8717.png)

6.烘焙好后，场景如图 所显示。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/15_%E5%AF%BC%E8%88%AA%E7%BD%91%E7%BB%9C%E5%AF%BB%E8%B7%AF_OffMeshLink/images/%E5%9B%BE%E7%89%8718.png)

7.为主角胶囊体添加脚本，如下所示

```C#
using UnityEngine;
using System.Collections;

public class PlayerController1 : MonoBehaviour {

    private NavMeshAgent agent;
    GameObject target;

    void Start()
    {
        //获取组件  
        agent = GetComponent<NavMeshAgent>();
        target = GameObject.Find("end point");
    }

    void Update()
    {
        agent.SetDestination(target.transform.position);
    }  
}
```

## 自定义移动过程

假如各位需要对越过OffMeshLink时候进行自己的控制，是需要另外写脚本的。我这里简单的介绍一下方法，有兴趣的朋友可以自己试试。

首先各位最好有用状态来控制角色的概念。比如人物可以分为站立、走路、跑步、上下楼梯、横向跳跃和往下掉落几种状态，针对NavMesh来说，人物简单的可以分为站立、正常的NavMesh寻路，和通过OffMeshLink移动几种状态。

先把 NavMesh Agent组件上的Auto Traverse Off Mesh Link选项取消。

然后，当人物在通过OffMeshLink移动的状态（可以用NavMeshAgent.isOnOffMeshLink来判断），获取到当前通过的OffMeshLink：

OffMeshLinkData link = NavMeshAgent.currentOffMeshLinkData;

这样你就能获取到link的开始点和结束点的坐标（link.startPos和link.endPos），这时候你的人物就可以用最简单的Vector3.Lerp来进行移动，当人物的位移到达了结束点的坐标，人物的OffMeshLink移动状态就可以结束，又重新变回正常寻路或者站立的状态了。在这个Vector3.Lerp的过程中，你可以随意的控制人物的爬行或者跳跃的动作。


如果制作的游戏项目与动画结合很密，使用此组件的概率将会增加！































