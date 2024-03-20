Unity

## 游戏时间

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Row : MonoBehaviour
{
    float timer = 0;
    // Start is called before the first frame update
    void Start()
    {
        //游戏开始到现在所花时间
        Debug.Log(Time.time);
        //时间缩放值
        Debug.Log(Time.timeScale);
        //固定时间间隔
        Debug.Log(Time.fixedDeltaTime);
        //上一帧到这一帧所用时间
        Debug.Log(Time.deltaTime);

    }

    // Update is called once per frame
    void Update()
    {
        //计时器
        timer=timer+Time.deltaTime;
        //如果大于十秒
        if (timer > 3) 
        {
            Debug.Log("大于三秒了");
        }
    }
}

```

## 路径权限Application

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Row : MonoBehaviour
{
    
    // Start is called before the first frame update
    void Start()
    {
        //游戏数据文件夹路径
        Debug.Log(Application.dataPath);
        //持久化文件夹路径
        Debug.Log(Application.persistentDataPath);
        //StreamingAssets文件夹路径（只读，配置文件）
        Debug.Log(Application.streamingAssetsPath);
        //临时文件
        Debug.Log(Application.temporaryCachePath);
        //控制是否在后台运行
        Debug.Log(Application.runInBackground);
        //打开链接
        Application.OpenURL("https://www.luogu.com.cn/");
        //退出游戏
        Application.Quit();
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}

```

## 场景

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;

public class NewBehaviourScript : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        //两个类，场景类，场景管理类
        SceneManager.LoadScene(1);
        //获取当前场景
        Scene scene = SceneManager.GetActiveScene();
        //场景名称
        Debug.Log(scene.name);
        //场景索引
        Debug.Log(scene.buildIndex);
        GameObject[] gos = scene.GetRootGameObjects();
        Debug.Log(gos.Length);
        //创建新场景
        Scene NewScene = SceneManager.CreateScene("NewScene");
        //当前场景个数
        Debug.Log(SceneManager.sceneCount);
        //卸载场景
        SceneManager.UnloadSceneAsync(NewScene);
        //加载场景
        SceneManager.LoadScene("My Scene", LoadSceneMode.Single);
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}

```

# 键鼠操作

```c#
void Update()
{
    //鼠标点击
    //按下鼠标 0左键，1右键，2滚轮
    if(Input.GetMouseButtonDown(0))
    {
        Debug.Log("按下左键");
    }
    //GetMouseDown持续点击
    if(Input.GetKeyDown(KeyCode.A)) 
    {
        Debug.Log("按下了A");

    }
    //GetKey持续按下
    //Getkeyup抬起
}

```

# 动画

## 旧版动画

```c#
void Update()
{
    if(Input.GetMouseButtonDown(0))
    {
      	GetComponent<Animation().Play("Right");
    }
}
```

# 移动

```c#
using System.Collections;
using System.Collections.Generic;
using Unity.Collections;
using UnityEngine;

public class NewBehaviourScript : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.F))
        {
            //触发pickup参数
            GetComponent<Animator>().SetTrigger("pickup");
        }
        //按键控制移动
        //水平轴
        float horizontal = Input.GetAxis("Horizontal");
        //垂直轴
        float vertical = Input.GetAxis("Vertical");
        //向量
        Vector3 dir = new Vector3(horizontal, 0, vertical);
        //面向向量
        transform.rotation = Quaternion.LookRotation(dir);//四元数中的方法：看向某个向量
        //切换跑步
        if(dir!= Vector3.zero)
        {
            //面向向量
            transform.rotation = Quaternion.LookRotation(dir);
            //播放跑步动画
            animator.SetBool("isrun", true);
            //朝向前方移动
            transform.Translate(Vector3.forward * 2 * Time.deltaTime);//每秒移动两米
        }
        else
        {
            animator.SetBool("isrun", false);
        }
        //随时获取Curve参数并打印出来
        //Debug.Log(animator.GetFloat("Curve"));
    }
}

```

# 事件

```c#
//先在动画中设置事件
void leftfoot()
{
    Debug.Log("左脚");
}
void rightfoot()
{
    Debug.Log("右脚");
```

# 反向动力学

```c#

//IK写到这个方法内
private void OnAnimatorIK(int layerIndex)
{
    animator.SetLookAtWeight(1);
    animator.SetLookAtPosition(target.position);
    //设置右手IK
    animator.SetIKPositionWeight(AvatarIKGoal.RightHand, 1);//位置权重
    animator.SetIKRotationWeight(AvatarIKGoal.RightHand, 1);//旋转权重
    animator.SetIKPosition(AvatarIKGoal.RightHand, target.position);
    animator.SetIKRotation(AvatarIKGoal.RightHand,target.rotation);
}
```

# 输入

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;//旧版输入框
using TMPro;//新版输入框

public class ButtonClick : MonoBehaviour
{
    public InputField InputField;//旧版输入
    public TMPro.TMP_InputField TMP_InputField;//新版输入
```

