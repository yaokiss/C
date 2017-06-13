## Animator 添加攻击特效事件

```c#
using UnityEngine;
using System.Collections;

public class attack : MonoBehaviour
{
    public GameObject Go;
    private Animator ai;
    RuntimeAnimatorController rac;  //声明一个动画控制器
    void Start()
    {
        ai = this.gameObject.GetComponent<Animator>();//获取动画器组件
        rac = ai.runtimeAnimatorController;//获取游戏对象动画器控制器

        AnimationEvent aie = new AnimationEvent();//创建一个动画事件
        aie.functionName = "Show";  //添加事件的方法名
        aie.time = 0.001f; //插入事件到动画的时间
        rac.animationClips[1].AddEvent(aie);//将事件添加到控制器的第一层（默认添加第一个动画为0）
        ai.Rebind(); //重新绑定动画器的所有动画的属性和网格数据

    }

    void Update()
    {

        AnimatorStateInfo asi = ai.GetCurrentAnimatorStateInfo(0);//获取动画控制器的基层（默认第一层为0）
        if (asi.IsName("idle"))      //当控制器播放“idle”动画时
            {
                if (Input.GetMouseButtonDown (0))
                {
                    ai.SetBool("isattack", true);
                }
            }
            if (asi.IsName("attack1"))
            {
                if (Input.GetMouseButtonDown(0))
                {
                    ai.SetBool("isattack", false);
                }
            }
    }

    void Show()
    {
        //Instantiate(Go,transform.position ,transform.rotation );
        GameObject a = Instantiate(Go, transform.position, transform.rotation) as GameObject;       
        Destroy(a, 1);      //删除克隆
    }
}


```

## 移动。缩放

```C#
using UnityEngine;
using System.Collections;

public class inputDemo : MonoBehaviour {
    public float Speed = 10.0f;
    public float RotationSpeed = 10.0f;

    public float H = 1.0f;
    public float V = 1.0f;

	void Start () {
	
	}
	
	// Update is called once per frame
	void Update () {
        float translation = Input.GetAxis("Horizontal") * Speed;
        float rotation = Input.GetAxis("Vertical") * RotationSpeed;

        translation *= Time.deltaTime;
        rotation *= Time.deltaTime;

        transform.Translate(translation ,0, 0);  //左右移动

        transform.Translate(0,0,rotation); //前后移动

        //transform.Translate(0,rotation ,0); //上下移动
        //transform.Rotate(rotation, 0, 0); //旋转

//-------------------------------------------------------------------

            float h =  H * Input.GetAxis("Mouse X");
            float v =  V * Input.GetAxis("Mouse Y");

            transform.Rotate(-v,h,0);
        //鼠标滚轮缩放
        if (Input.GetAxis("Mouse ScrollWheel") < 0)
        {
            if (Camera.main.fieldOfView <= 100)
                Camera.main.fieldOfView += 2;
            if (Camera.main.orthographicSize <= 20)
                Camera.main.orthographicSize += 0.5F;
        }
        //Zoom in  
        if (Input.GetAxis("Mouse ScrollWheel") > 0)
        {
            if (Camera.main.fieldOfView > 2)
                Camera.main.fieldOfView -= 2;
            if (Camera.main.orthographicSize >= 1)
                Camera.main.orthographicSize -= 0.5F;
        }       
	}
}

```
```C#
using UnityEngine;
using System.Collections;

public class CameraDemo : MonoBehaviour {

	
	void Start () {
	
	}
	
	// Update is called once per frame
	void Update () {
       /*
        if((transform.localScale == new Vector3 (1,1,1)))
        {
            transform.localScale = new Vector3(1,1,1);
        }*/

        if ((Input.GetAxis("Mouse ScrollWheel") > 0) )
        {
            transform.localScale += new Vector3(1, 1, 1);
        }
        if (Input.GetAxis("Mouse ScrollWheel") < 0 )
        {
            transform.localScale -= new Vector3(1, 1, 1);
            if((transform.localScale == new Vector3 (0,0,0)))
            {
                transform.localScale = new Vector3(1, 1, 1);
            }
        }
	}
}

```

```C#
using UnityEngine;
using System.Collections;

public class CollisionDemo : MonoBehaviour {
    
    void OnCollisionEnter(Collision c)
    {
        if (c.gameObject.tag == "Ball")
        {
            print("进入碰撞");
        }
    }
    void OnCollisionStay(Collision c)
    {
        if (c.gameObject.tag == "Ball")
        {
            print("逗留");
        }
    }
    void OnCollisionExit(Collision c)
    {
        if (c.gameObject.tag == "Ball")
        {
            print("退出碰撞");
        }
    }

    //当进入触发器
    void OnTriggerEnter( Collider Co )
    {
        if(Co.gameObject .tag == "Boo")
        {
            print("触发"); 
        }
    }
    //当退出触发器
    void OnTriggerExit(Collider Co)
    {

    }
    //当逗留触发器
    void OnTriggerStay(Collider Co)
    {

    }
}

```






































