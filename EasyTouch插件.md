## 摇杆的创建

从参考资料中下载EasytTouch摇杆插件，并导入到Unity编辑器中.

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403231833.jpg)

添加一个摇杆

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403231242.jpg)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403231604.jpg)

如果EasyTouch没存在场景中，会自动创建

在Inspector面板中设置摇杆相关参数。

在JoyStick组件的界面上可以分为四项参数设置。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403231701.jpg)

* Proerties: 摇杆属性设置
* Position & Size ： 摇杆位置及大小
* Joystick Axes properties & Events: 摇杆轴属性及事件
* Joystick: 纹理图片

JoyStick Properties设置

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403232146.jpg)

* Dynamic joystick: 是否为动态摇杆，即在按下手指的位置出现摇杆。
* Anchor: 预置位置 默认Lower Left(左右角)
* Offset：偏移量
* 其它:调整摇杆的大小等。

Joystic Axes properties & Events设置

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403232622.jpg)

* 此项用于设置摇杆开户的轴及摇杆交互类型.
* Interaction Type:交互类型

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403233022.jpg)

  * Direct 直接拖动物体到启用轴上去，选择交互效果。
  * Event Notification ： 事件通知方式，较为常用。


Joystick Textures设置

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403233308.jpg)

此项是用来更改摇杆的样子


案例


利用Event Notification交互方式实现对游戏对象物位移控制。

将摇杆的交互方式修改为Event Notification类型，并将轴设置中各轴的速度Speed 修改为2

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/10_%E6%91%87%E6%9D%86%E6%8F%92%E4%BB%B6EasyTouch/images/20170403234108.jpg)


新建Cube和程序MyET.cs,并挂载到Cube对象上,编写程序如下:

```C#
  using UnityEngine;
  using System.Collections;

  public class MyET : MonoBehaviour {
  	/// <summary>
  	/// 用于存储摇杆移动过程中的位移
  	/// </summary>
  	float vx;
  	float vy;
  	// Use this for initialization
  	void Start () {
  		//添加事件，订阅摇杆的移动事件
  		EasyJoystick.On_JoystickMove += OnJoystickMoveHandler;
  		//订阅移动结束事件
  		EasyJoystick.On_JoystickMoveEnd+=OnJoystickEndHandler;
  	}

  	void OnJoystickEndHandler(MovingJoystick move){
  		//移动结束时，将各轴移动量设定为0
  		vx = vy = 0;
  	}
  	void OnJoystickMoveHandler (MovingJoystick move) {
  		//获取摇杆各轴的输入值
  		vx = move.joystickValue.x;
  		vy = move.joystickValue.y;
  	}

  	void Update(){
  		//根据输入的vx,vy对物体进行位移
  		this.transform.Translate (new Vector3(vx, vy, 0)*Time.deltaTime);
  	}
  }
```





















