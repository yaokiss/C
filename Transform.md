Transform组件是每个游戏对象必须有的一个组建，因为unity3d是面向组建开发的一款游戏引擎。这个组件掌管了游戏对象在三维空间中的位置，旋转，绽放等。

Transform常用的属性

属性	                 说明

position	        在世界坐标系中的位置

localPostion	    相对于父级的变换位置

eulerAngles	      以欧拉角形式表示的旋转角度

localEulerAngles	相对于父级物体的旋转欧拉角度

rotation	        在世界坐标系中物体变换的旋转角度作为Quaternion存储

parent	          返回物体变换的父级

root	            返回最高层次的物体变换

案例1

通过代码查看这些属性的区别

```
Debug.Log("position " + transform.position); //世界坐标的位置
Debug.Log("localPosition " + transform.localPosition); //相对于父位置的坐标 即把父物体当作自己的中心

Debug.Log("eulerAngles " + transform.eulerAngles);//世界坐标欧拉⾓度

Debug.Log("localEulerAngles " + transform.localEulerAngles);//相对于⽗级的变换的旋转欧拉⾓度

Debug.Log("localScale " + transform.localScale);//相对于父位置的缩放

Debug.Log("localRotation " + transform.localRotation);//相对于父位置的旋转

Debug.Log("rotation " + transform.rotation);//世界坐标的旋转
```
上面提到了父位置？那是什么意思呢？

现在创建两个cube 命名为cube1和cube2 把cube2作为cube1的子对象，如图。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/04_Transform/images/jeUbee6.jpg)


可以看到，cube1的坐标(1,0,0) cube2的坐标为(0,0,5)

那么通过transform.localPosition获取cube2的坐标则为(0,0,5)

如果用transform.position获取cube2的坐标则为(1,0,5)

那么写个脚本测试下。写个脚本挂载到cube2上

在脚本的Start方法中如下写
```
void Start()
{
  Debug.Log("cube2的世界坐标为：" + transform.position);
  Debug.Log("cube2的本地坐标为：" + transform.localPosition);
}
```
运行后看结果

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/04_Transform/images/eMviQr.jpg)


因为：cube2把父对象（Cube1）当作了自己的的中心。所以是(0,0,5)，那它的世界坐标则为(1,0,5)，知道了这个position那localRotation也是同样的道理

但有没有注意到。这里的欧拉角(eulerAngles),rotation和Rotate()，都是用于旋转，那他们有什么区别呢。刚开始我也是犯糊涂

Rotate()方法需要一个vector3三维向量,rotation是用四元素旋转（Quaternion）

Transform.Rotate

应用一个欧拉角的旋转角度，eulerAngles.z度围绕z轴，eulerAngles.x度围绕x轴，eulerAngles.y度围绕y轴（这样的顺序）。

如果相对于留空或者设置为Space.Self 旋转角度被应用围绕变换的自身轴。（当在场景视图选择物体时，x、y和z轴显示）如果相对于 Space.World 旋转角度被应用围绕世界的x、y、z轴。

Transform.rotation 旋转角度

在世界空间坐标物体变换的旋转角度作为Quaternion储存。

Untiy作为四元数内部储存旋转角度。旋转一个物体，使用Transform.Rotate，使用Transform.eulerAngles为设置作为欧拉角的旋转角度。
```C#
//重设世界的旋转角度
using UnityEngine;
using System.Collections;

public class example : MonoBehaviour {
	public void Awake() {
		transform.rotation = Quaternion.identity;
	}
}
```
//平滑倾斜物体向一个target旋转
```C#
using UnityEngine;
using System.Collections;

public class example : MonoBehaviour {
	public float smooth = 2.0F;
	public float tiltAngle = 30.0F;
	void Update() {

		float tiltAroundZ = Input.GetAxis("Horizontal") * tiltAngle;
		float tiltAroundX = Input.GetAxis("Vertical") * tiltAngle;
		Quaternion target = Quaternion.Euler(tiltAroundX, 0, tiltAroundZ);
    	//向target旋转阻尼
		transform.rotation = Quaternion.Slerp(transform.rotation, target, Time.deltaTime * smooth);
	}
}
```
Transform.eulerAngles 欧拉角

旋转作为欧拉角度。x、y、z角代表绕z轴旋转z度，绕x轴旋转x度，绕y轴旋转y度（这个顺序）。

仅使用者这个变量读取和设置角度到绝对值。不要递增它们，当超过角度360度，它将失败。使用Transform.Rotate替代。
```C#
using UnityEngine;
using System.Collections;

public class example : MonoBehaviour {
	public float yRotation = 5.0F;
	void Update() {
    //指定一个绝对使用欧拉角的旋转角度
		yRotation += Input.GetAxis("Horizontal");
		transform.eulerAngles = new Vector3(10, yRotation, 0);
	}
	public void Awake() {
    //打印绕世界x轴的旋转角度
		print(transform.eulerAngles.x);
    //打印绕世界y轴的旋转角度
		print(transform.eulerAngles.y);
    //打印绕世界z轴的旋转角度
		print(transform.eulerAngles.z);
	}
}
```
不要分别设置欧拉角其中一个轴（例如： eulerAngles.x = 10; ），因为这将导致偏移和不希望的旋转。当设置它们一个新的值时，要同时设置全部，如上所示。Unity会从Transform.rotation这个四元组结构中转换角度到欧拉角的表达方式，或者反过来。

欧拉角(eulerAngles）旋转很好理解。当你改变Transform组建中的 x,y,z的角度。就是改变其欧拉角

现在来看看rotation属性和Rotate()方法之间有什么区别

我认为通过测试是对两者差异的最好理解。

先看Rotate()方法,在场景中创建一个Capsule，写个脚本。代码如下
```
void Update(){
  transform.Rotate(Vector3.up  * 5);
}
```
运行看看效果:

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/04_Transform/images/fAN7Jj.gif)

可以看到对象是旋转一直是在累加5,如果你感觉不出来。我这里调试。一帧一帧给你看

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/04_Transform/images/6zyAjeM.gif)


然后用旋转同样的角度。测试rotation属性
```
 transform.rotation = Quaternion.Euler(Vector3.up  * 5);
```

同样看效果

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/04_Transform/images/BnIzMv6.gif)

上图可以看出，Capsule旋转到5就不动了。也就是每次旋转动是同样的值，

所以：我的理解是：

Rotate()方法是：旋转多少度。在原有的基础上累加，即旋转了多少角度。又旋转了多少角度

rotation属性是：旋转到某个角度，就是是在update中每帧都执行。但每次旋转到的角度动是5，所以是旋转到5度。一直都是

比如你只想让他旋转到多少,用rotation;假如想让他一直转,可以用Rotate

rotation直接改变了数值,以达到旋转效果

Rotate应用一个的旋转角度每秒1度慢慢的旋转物体
当然:rotation()还可以通过插值旋转，
```C#
using UnityEngine;
using System.Collections;

public class example : MonoBehaviour {
	public float smooth = 2.0F;
	public float tiltAngle = 30.0F;
	void Update() {

		float tiltAroundZ = Input.GetAxis("Horizontal") * tiltAngle;
		float tiltAroundX = Input.GetAxis("Vertical") * tiltAngle;
		Quaternion target = Quaternion.Euler(tiltAroundX, 0, tiltAroundZ);
    	//向target旋转阻尼
		transform.rotation = Quaternion.Slerp(transform.rotation, target, Time.deltaTime * smooth);
	}
}
```

课后练习题

使用世界坐标转屏幕坐标完成一个血量条的显示效果。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/04_Transform/images/20170331195846.jpg)

使一个游戏物体向前移动五个单位后再旋转180°返回原来位置。

编写代码让一个游戏物体按照菱形的路线规则的运动，速度平均。

水平轴向控制物体Y轴旋转，垂直轴向控制物体Z轴移动

查阅Input类的GetAxis(“Mouse X”)方法的使用，实现鼠标转动物体。
