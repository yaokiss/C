# 移动与旋转

课程目标

规范化向量

求向量长度

求两个物体的距离

在Unity中，控制物体或主角的移动和旋转是一块非常重要的内容。很多相关的概念不是很容易理解。翻阅其API，很多知识点或函数方法众多，Unity本身有非常丰富的API函数，而且有个特点是往往达到同一个需求的函数方法会有很多个，这对初学者而言很容易造成知识的混乱。本章节就对这些众多的API函数进一步的梳理和归纳，从而深入了解最基本且易混淆的概念，比如Transform、Translate、Rotate、Rotation、Position；Vector3（三维向量）、Quaternion（四元数）、角度、欧拉角等概念。并且会尝试着从位移、缩放、角度、旋转、朝向、转换几个方面来分类讲解。

3.1概念

1、Transform 变换：这是一个类。也是代表一个组件,表示物体的位置、旋转和缩放。在Inspector面板中，我们可以看到每个物体（包括空物体）都会至少有一个这样的组件，其中就包含了位置、旋转、缩放3个属性。

2、Vector3三维向量：表示3D的向量和点。包含位置、方向（朝向）、欧拉角的信息，也包含做些普通向量运算的函数。

3、Quaternion[kwə’tɜːnɪən] 四元数，用于表示旋转，Unity内使用Quaternion表示所有旋转。在电脑图形学中用于表示物体的旋转，在unity中由x,y,z,w 表示四个值。四元数不会产生万向节死锁并且能够很容易被插值。
在Unity里，tranform组件有一个变量名为rotation，它的类型就是四元数。

4、欧拉角：用来确定定点转动刚体位置的3个一组独立角参量，用来表示旋转角度，为欧拉首先提出而得名。

声明：
```C#
 声明四元数：
 Quaternion q1 = this.transform.rotation;			
 q1 = this.transform.rotation;//四元数

 声明Vector3：
 Vector3 v1 = new Vector3(0, 0, 0);
 v1 = this.transform.eulerAngles;//Vector3的欧拉角

 Vector3 v2 = new Vector3(0, 0, 0);
 v2 = this.transform.position;
```
注：欧拉角的返回值为Vector3类型的

1、Vector3.normalized规范化

* 非静态属性；
* 返回类型为Vector3；
* 返回的向量与原向量的方向相同，长度为1（只读）；原向量不变；
* 若原向量太小，则返回零向量；
* Vector3 v1 = this.transform.position.normalized;等价于：
* Vector3 v2 = Vector3.Normalize(this.transform.position);
* 不管长度为多少。都以单位长度为1进行规范

2、Vector3.Normalize()规范化

* 静态函数；
* 返回类型为void；
* 使原向量改变，长度变为1，方向与原向量相同；
* 若原向量太小，则使原向量为零向量；
* Vector3 v1 = this.transform.position.normalized;等价于：
* Vector3 v2 = Vector3.Normalize(this.transform.position);

后面会举例规范化的作用

3、Vector3.magnitude 长度

* 返回向量的长度（只读）。即只有大小，没有方向。
* 不管方向为多少，只计算他的长度
* 返回类型为float；
* Vector3.magnitude向量的长度是(x*x+y*y+z*z)的平方根。
```
 print(Vector3.Magnitude(new Vector3(3, 4, 0)));
```
Vector3.SqrMagnitude

返回向量的长度的两次方。 向量的长度是用勾股定理计算出来的，计算机计算两次方和开跟的运算量比加减法要费时的多。所以如果是想比较两个向量的长度的话，用sqrMagnitude可以快很多。
4、类属性：

* 1、Vector3.zero：Vector3(0, 0, 0)的简码。eg：this.transform.position = Vector3.zero;
* 2、Vector3.one：Vector3(1, 1, 1)的简码。
* 3、Vector3.right：Vector3(1, 0, 0)的简码。即x轴。
* 4、Vector3.up：Vector3(0, 1, 0)的简码。即y轴。比较（this.transform.up）。
* 5、Vector3.forward：Vector3(0, 0, 1)的简码。即z轴。
（可利用左手坐标系判断）。

5、Vector3.Distance() 距离

* 返回a和b之间的距离。
* static function Distance (a : Vector3, b : Vector3) : float
* Vector3.Distance(a,b) 等同于(a-b).magnitude.
Eg：
```c#
 public Transform CubeA;
 public Transform CubeB;
 void Start()
{
	float distance1 = (CubeB.position - CubeA.position).magnitude;
	float distance2 = Vector3.Distance(CubeA.position, CubeB.position);

	Debug.Log(distance1);
	Debug.Log(distance2);
}
```
课堂练习

使用Vector3.magnitude计算两个向量的长度
创建两个物体,计算这两个物体的距离
已知X向量的归一化后为（0.5，0.6，0.7），得知它距离原点长度的平方是77，求出X向量。
已知物体A在（0，0，0）点上，算出朝坐标（2，3，6）方向，长度为49的点坐标。（可以尝试诞生一个物体在该坐标上）
物体B在正常巡逻（菱形移动）当控制玩家A走到B周围5个单位范围内，B不移动并看向玩家A，A远离时B继续巡逻。
