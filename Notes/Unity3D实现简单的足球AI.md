---
title: Unity3D实现简单的足球AI
authors: Ethan Lin
year: 2023-05-14 
tags:
  - 日期/2023-05-14 
  - 类型/笔记 
  - 来源/转载 
---


# Unity3D实现简单的足球AI









# 来源

> [CSDN：Unity 如何写一个足球运动员AI（一）](https://blog.csdn.net/Roadlun/article/details/80314642)



# 相关代码

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
 
public class PlayerStateCon : MonoBehaviour
{
 
    //这个脚本负责设置球员AI的属性：移速，冷却，力度，智慧，灵敏等
    //并且负责定义所有状态对应的方法方法，如射门，传球，带球，待传球，追球，抢断，回防，跑位等
 
    //球员属性
    public float speed;     //速度
    public float cooling;   //冷却
    public float smart;     //智能（做出正确选择的概率）
    public float sensitive; //灵敏（思考时间）
    public float power;     //力量
    private Vector3 attackDir;  //当前球员的进攻方向
    public Transform ballTran;
    Rigidbody ballRig;          //球的刚体
    public Transform blueShootDir;  //蓝方射门方向
    public Transform redShootDir;   //红方射门方向
 
    public enum Team
    {
        Blue = 0,
        Red = 1
    };
    public Team team;
    //球员状态枚举
    public enum PlayerState
    {
        //进攻
        Shoot = 0,                 //射门
        Dribbling = 1,             //带球           
        Pass = 2,                  //传球
        WatiePass = 3,              //待传
        //防守
        Steals = 10,               //抢断
        ReturnDefense = 11,        //回防
        //通用
        Chase = 20,               //追球
        RunPosition = 21,         //跑位
        KickForward, //向前踢
        //等待守门员开球
        Static = 30,              //静止              不写
        //开局开球              
        WaitInPosition = 40         //在固定位置等待      不写
        
 
    };
    public PlayerState playerState;     //当前球员状态
 
    private void Start()
    {
        ballRig = ballTran.GetComponent<Rigidbody>();  //获取刚体
    }
    private void Update()
    {
        PersistenceState();
    }
    //各种方法
 
    //根据当前状态执行(都是持续状态)
    //要处理的持续状态有:带球，追球，静止
    void PersistenceState()
    {
        switch (playerState)
        {
            case PlayerState.Shoot:
                Dribbling();
                break;
            case PlayerState.Chase:
                Chase();
                break;
            case PlayerState.Static:
                break;
        }
    }
 
    //精确射门，（如果方向不对，则不射门）
    //获取碰撞体半径
    public Transform colliderCenter;    //碰撞中心    这个是自己定义的 再球员前方设置一个Transform即可
    public float colliderRadius;    //碰撞半径
    public void Shoot()
    {
 
        //bool siShoot=false;  //是否射门
        //Rigidbody ballRig;
        //判断范围内是否有球
        //前方是否正确
        //条件满足 射门                         
        //获取半径内所有碰撞体，如果是球，则加一个力，力的方向是球员到球（可上移）
 
        if (!IsHoldingBall())
        {
            Debug.Log("没有持球");
            
            return;
        }
        //switch case性能比if else好
        switch (team)
        {
            case Team.Blue:
                if (Vector3.Dot(Vector3.left, transform.forward) > 0)
                {
                    // Debug.Log("方向不对1");
                    GetComponent<PlayerStateTrigger_Con>().MonitoringTrigger();
                    return;
                }
                break;
            case Team.Red:
                if (Vector3.Dot(Vector3.left, transform.forward) < 0)
                {
                    // Debug.Log("方向不对2");
                    GetComponent<PlayerStateTrigger_Con>().MonitoringTrigger();
                    return;
                }
                break;
        }
        //两个条件都通过，可以踢球了
        Vector3 kickVec = ballRig.transform.position - transform.position;
        ballRig.AddForce(kickVec.normalized * power);
        // Debug.Log("踢球了");
        //ballRig = null;     //将刚体置空
    }
    //盲目射门（直接射门）
    public void BlindShoot()
    {
        //红方向红方射门点射门
        //兰芳向兰芳射门点射门
        if (team==Team.Blue)
        {
            ballRig.AddForce((blueShootDir.position - ballTran.position).normalized * power);
        }
        else
        {
            ballRig.AddForce((redShootDir.position - ballTran.position).normalized * power);
        }
    }
 
    //带球
    //推着球往前走
    public void Dribbling()
    {
        //条件如果方向正确
        //如果球在前方
        //如果有球
        //推着球向前移动
       
        if (!IsHoldingBall())
        {
            //Debug.Log("没有持球");
            //Debug.Log( "状态触发组件  "+GetComponent<PlayerStateTrigger_Con>());
            GetComponent<PlayerStateTrigger_Con>().StateReset();  //状态重置
            return;
        }
        //switch case性能比if else好
        switch (team)
        {
            case Team.Blue:
                if (Vector3.Dot(Vector3.left, transform.forward) > 0)
                {
                    // Debug.Log("方向不对1");
                    return;
                }
                break;
            case Team.Red:
                if (Vector3.Dot(Vector3.left, transform.forward) < 0)
                {
                    // Debug.Log("方向不对2");
                    return;
                }
                break;
        }
        //条件符合，推着球向前走，方向为当前方向，角度为插值
        Debug.Log("正在带球");
        transform.position += -transform.right * speed*Time.deltaTime;
        //Debug.Log("正在带球");
    }
 
    //传球
    //如果前方有队友，且与队友的角度不超过60°（全角），
    //且射出一个射线，射线没有击中对方球员，则传球
    public float findTeammateSphereRaidus;      //用来找队友的球的半径
    Transform teammateTran;
    public void Pass()
    {
        if (!IsHoldingBall())
        {
            Debug.Log("没有持球");
            return;
        }
 
        //先获得队友信息
        Collider[] allColls = Physics.OverlapSphere(transform.position, findTeammateSphereRaidus);
        foreach (Collider item in allColls)
        {
            if ( team==Team.Blue&& item.tag == "BlueNPC")
            {
                teammateTran = item.transform;
                break;      //这一步表示，不论有多少个队友，只查找集合的第一个，并返回
            }
            if (team==Team.Red&&item.tag=="RedNPC")
            {
                teammateTran = item.transform;
                break;
            }
        }
        if (teammateTran==null)
        {
            Debug.Log("没找到队友");
            GetComponent<PlayerStateTrigger_Con>().MonitoringTrigger();
            return;
        }
        //判断角度
       // float angle=Vector3.Angle((teammateTran.position - transform.position), -transform.right);
       // if (angle>60&&angle<-60)
       // {
       //     Debug.Log("角度不对");
       //     GetComponent<PlayerStateTrigger_Con>().MonitoringTrigger();
       //     return;
       // }
        Ray ray = new Ray(transform.position, (teammateTran.position - transform.position));
 
 
        
        RaycastHit hit;
        
        if (Physics.Raycast(ray,out hit,Mathf.Infinity))    //射一条无穷大的射线
        {
            //如果射线碰到对方选手，则返回
            if (team==Team.Blue&&hit.collider.tag=="RedNPC")
            {
                Debug.Log("蓝方选手射线射到红方选手");
                GetComponent<PlayerStateTrigger_Con>().MonitoringTrigger();
                return;
            }
            if (team==Team.Red&&hit.collider.tag=="BlueNPC")
            {
                Debug.Log("红方选手射线射到蓝方选手");
                GetComponent<PlayerStateTrigger_Con>().MonitoringTrigger();
                return;
            }
        }
        else
        {
            //Debug.Log("射线有问题");
            //GetComponent<PlayerStateTrigger_Con>().MonitoringTrigger();
            //return;
        }
        //条件达成 可以传球
        Debug.Log("传球 "+gameObject.name);
        ballRig.AddForce((teammateTran.position - transform.position).normalized * power);
 
        teammateTran = null;  //执行完，必定置空
    }
 
    //等待传球
    void WaitPass()
    {
        //指令 原地等待
        //注视球飞过来 (后期再解决旋转问题，目前先不写)
        
    }
 
    //抢断
    void Steals()
    {
        //抢断：用来干扰对方进攻，
        //如果球在范围内，并且如果当前面向地方大门，则踢一脚
        if (!IsHoldingBall())
        {
            Debug.Log("球不在范围内，无法抢断");
            return;
        }
        if (team==Team.Blue&&Vector3.Dot(-transform.right,Vector3.left)<0)
        {
            //蓝队 方向错了，返回
            Debug.Log("蓝队队员 方向错误，无法抢断");
            return;
        }
        if (team==Team.Red&&Vector3.Dot(-transform.right,Vector3.left)>0)
        {
            Debug.Log("红队队员 方向错误，无法抢断");
            return;
        }
        //条件通过 可以抢断
        ballRig.AddForce((ballTran.position - transform.position).normalized * power);
        Debug.Log("抢断成功");              
    }
 
    //回防
    public void ReturnDefense()
    {
        //当对手持球进攻时
        //当前角色回防，以规定速度向
        if (team==Team.Blue)
        {
            transform.position += Vector3.left * speed * Time.deltaTime;
            //Debug.Log("正在回防");
        }
        else
        {
            transform.position += Vector3.right * speed * Time.deltaTime;
        }
 
    }
 
    //追球
    public void Chase()
    {   
        //追逐球
        transform.position += (ballTran.position - transform.position).normalized * speed*Time.deltaTime;
       // Debug.Log("正在追球");
    }
 
    //跑位
    //根据球的位置判断跑向哪个方向，此处写成瞬发方法而非状态方法，
    //因为如果跑位的时候球的动向转变，但角色还是再跑位，显得很蠢
    //左右移动
    public float runPositionForce;
    public void RunPosition()
    {
        int a = Random.Range(0, 1);
        if (a==0)
        {
            GetComponent<Rigidbody>().AddForce(-transform.right * runPositionForce);
        }
        else
        {
            GetComponent<Rigidbody>().AddForce(transform.right * runPositionForce);
        }
        //瞬发方法生效，重置状态;
       // GetComponent<PlayerStateTrigger_Con>().StateReset();
    }
 
    //向前踢
    //当球进入触发范围时，球员有概率强前踢，如果时红方，就像Vector3.right方向踢，
    //如果蓝方就像Vector3.left方向踢
    public void KickForward()
    {
        //Debug.Log("")
        if (team==Team.Blue)
        {
            ballRig.AddForce(Vector3.left * power);
        }
        else
        {
            ballRig.AddForce(Vector3.right * power);
        }
    }
 
 
    //判断当前对象是否持球，如果没有持球，则不能进行带球，传球，运球
    bool IsHoldingBall()
    {
        return (colliderCenter.position - ballTran.position).magnitude < colliderRadius;    //球距离没有超过持球半径，默认持球（treu）
    }
}

```