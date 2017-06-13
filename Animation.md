## 动画系统

模型大小

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404221959.jpg)

动画切割方法

将参考资料中的 Animation动画素材导入到Unity项目中，选中Charactor.fbx文件，在Inspector面板中进行相应设置。

Rig标签设置如下:

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404224403.jpg)

Animation标签设置如下:

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404222353.jpg)

选中Import Animation项后，点击Apply按钮，将会出现如下界面。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404222505.jpg)

在Charactor.fbx同目标中，打开animations文件，此文件中记录着此模型各动画开始帧和结束帧，（通常该文件会由动画制作人员提供），接下来，我们需要根据此文件内容进行动画切割。

选中Clips中的Take 001项，会出现以下界面。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404222744.jpg)

将Take001修改为 idle,并将Start设定为 0, End设定为 30,然后点击底部的Apply按钮,并可以通过底部的预览窗口进行动画查看。(如果没有此窗口，请点击最底部的横条)

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404223604.jpg)

如果希望此动画能够循环播放，可以将Warp Mode 设定为Loop.

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404225403.jpg)

然后点击Clips下的 “+” 继续添加新动画,指定开始与结束帧，点击Apply.

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404223331.jpg)

通过上面的操作按Animations.txt文件内容切割动画

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404224102.jpg)

## 动画的控制

动画切割完成后，我们可以通Animation组件提供的方法对动画进行控制。

将切割好动画的模型拖动到场景中，会发现模型上挂载的Aniamtion组件，并且组件中的animations数组中存放的是刚刚切割好的动画片段。

![](https://nts.newbieol.com/static/k25/02_%E6%B8%B8%E6%88%8F%E5%BC%95%E6%93%8E%E6%A0%B8%E5%BF%83/13_%E5%8A%A8%E7%94%BB%E7%B3%BB%E7%BB%9F_Animation/images/20170404225605.jpg)

## 动画切换

创建一个C#脚本MyAni，挂载到模型上，并编写以下脚本。


```C#
using UnityEngine;
using System.Collections;

public class MyAni : MonoBehaviour {

	private Animation ani;
	// Use this for initialization
	void Start () {
		ani = this.gameObject.GetComponent<Animation> ();

	}

	// Update is called once per frame
	void Update () {
		if (Input.GetMouseButtonDown (0)) {
			//设定动画为循环方式
			ani.wrapMode = WrapMode.Loop;
			//将动画切换到walk
			ani.CrossFade ("walk");
		}
		if(Input.GetMouseButtonDown(1)){
			//设定动画为循环方式
			ani.wrapMode = WrapMode.Loop;
			//将动画切换到idle
			ani.CrossFade ("idle");
		}
	}
}
```


```C#
using UnityEngine;
using System.Collections;

public class AnimationsDemo : MonoBehaviour
{
    public Animation ai;

	// Use this for initialization
	void Start () {
	    ai = this.gameObject .GetComponent <Animation>();
	}
	
	// Update is called once per frame
	void Update () {
        float H = Input.GetAxis("Horizontal");
        float V = Input.GetAxis("Vertical");
        transform.Translate(0,0,V);
        transform.Translate(H, 0, 0);

        if(Input.GetKey(KeyCode.W))
        {
            transform.Translate(Vector3.forward * Time.deltaTime * 10);
            ai.Play("walk");
        }
        if (Input.GetKey(KeyCode.S))
        {
            transform.Translate(Vector3.back * Time.deltaTime * 10);
            ai.Play("walk");
        }
        if (Input.GetKey(KeyCode.A))
        {
            transform.Translate(Vector3.left * Time.deltaTime * 10);
            ai.Play("walk");
        }
        if (Input.GetKey(KeyCode.D))
        {
            transform.Translate(Vector3.right * Time.deltaTime * 10);
            ai.Play("walk");
        }


        
	    if(Input.GetMouseButton(0))
        {
            ai.CrossFade("attack1");
        }
        if (Input.GetMouseButton(1))
        {
            ai.CrossFade("attack2");
        }
        if(Input.GetKey (KeyCode.Space ))
        {
            ai.Play("idle");
        }
        
            
	}
}

```


```C#
using UnityEngine;
using System.Collections;

public class AnimationsDemo1 : MonoBehaviour {
    public AnimationClip _idle;
    public AnimationClip _attack1;
    public AnimationClip _attack2;
    public AnimationClip _attack3;
    public AnimationClip _jump;
    public AnimationClip _run;
    public AnimationClip _Dodge;
    public AnimationClip _die;

    //宽，高
    public float scaleW = 1f;
    public float scaleH = 1f;

	void Update () {
        scaleW = (float)Screen.width / 800;//计算宽度缩放比例
        scaleH = (float)Screen.height / 480; //计算高度的缩放比例

        //if(!GetComponent <Animation>().isPlaying)
        //{
        //    GetComponent<Animation>().CrossFade("idle");
       // }
	}

    void OnGUI()
    {
        GUI.skin.button.fontSize = (int)(10 * scaleW);//按钮字体大小设置

        if(GUI.Button(new Rect(scaleW,10 * scaleH,50 * scaleW,20 * scaleH),"静止"))
        {
            GetComponent<Animation>().CrossFade("idle");
        }
        if (GUI.Button(new Rect(scaleW, 35 * scaleH, 50 * scaleW, 20 * scaleH), "直拳"))
        {
            GetComponent<Animation>().CrossFade("attack1");
        }
        if (GUI.Button(new Rect(scaleW, 60 * scaleH, 50 * scaleW, 20 * scaleH), "轻拳"))
        {
            GetComponent<Animation>().CrossFade("attack2");
        }
        if (GUI.Button(new Rect(scaleW, 85 * scaleH, 50 * scaleW, 20 * scaleH), "重拳"))
        {
            GetComponent<Animation>().CrossFade("attack3");
        }
        if (GUI.Button(new Rect(scaleW, 110 * scaleH, 50 * scaleW, 20 * scaleH), "跳跃"))
        {
            GetComponent<Animation>().CrossFade("jump");
        }
        if (GUI.Button(new Rect(scaleW, 135 * scaleH, 50 * scaleW, 20 * scaleH), "奔跑"))
        {
            GetComponent<Animation>().CrossFade("run");
        }
        if (GUI.Button(new Rect(scaleW, 160 * scaleH, 50 * scaleW, 20 * scaleH), "躲闪"))
        {
            GetComponent<Animation>().CrossFade("Dodge");
        }
        if (GUI.Button(new Rect(scaleW, 185 * scaleH, 50 * scaleW, 20 * scaleH), "死亡"))
        {
            GetComponent<Animation>().CrossFade("die");
        }
    }
}

```

```C#

using UnityEngine;
using System.Collections;

public class EffectsDemo : MonoBehaviour
{
    Animation ai;       //动画声明
    AnimationClip aic;  //剪辑声明
    public GameObject Go;
	void Start () {
        ai = this.gameObject.GetComponent<Animation>();
        //aic = ai.GetClip("jump");
        //aic = ai.GetClip("attack1");
        //aic = ai.GetClip("run");
        AnimationEvent aie = new AnimationEvent();
        //aie.time = aic.length * Time.deltaTime ;
        //aie.functionName = "Show";
        //aie.functionName = "Show1";
        //aie.functionName = "Show2";


        aic.AddEvent(aie);
	}
	
	void Update () {
	
	}
    void Show()
    {
        Instantiate(Go);
        
    }
    void Show1()
    {
       transform.Translate(0,5 *Time.deltaTime ,0);
    }
    void Show2()
    {
        transform.position = Vector3.MoveTowards(transform.position ,Vector3.forward * 100 , Time.deltaTime);
    }
    
    
}
```

```C#
using UnityEngine;
using System.Collections;

public class Moveingrun : MonoBehaviour {
    public float SpeedPlay;
    private Vector3 V;
    private bool bo;
    //Animation ai;
    //AnimationClip aic;
	void Start () {
	    //ai = this.gameObject .GetComponent <Animation>();
        
	}
	
	void Update () {
	    if(Input.GetMouseButton(0))
        {
            Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition);
            RaycastHit hit = new RaycastHit();
            if(Physics.Raycast(ray,out hit))
            {
                if(hit.collider .name == "Plane")
                {
                    V = hit.point ;
                    //V.y = 0.5f;
                    bo = false ;
                }
            }
        }
        MoveTo(V);

	}
    private void MoveTo(Vector3 vv)
    {
        if(!bo)
        {
            Vector3 v3 = vv - transform.position;
            transform.position += v3.normalized * SpeedPlay * Time.deltaTime;
            GetComponent<Animation>().CrossFade("run");
            if(Vector3.Distance (vv,transform .position ) < 0.1f)
            {
                bo = true;
                transform.position = vv;
            }
        }
        this.transform.LookAt(vv);
       // this.transform.position = Vector3.MoveTowards(this.transform.position, Input.mousePosition, Time.deltaTime * SpeedPlay);
    }
}

```







