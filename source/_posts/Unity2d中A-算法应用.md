---
title: Unity2d中A*算法应用
date: 2021-10-18 22:17:14
tags: A星算法应用
categories: C++
---

﻿# Unity2d项目A*插件实时添加障碍物

## 一、实现步骤

   可以去B站搜教程，详细的就不说了，
   主要是最近在做一个塔防迷宫，
   敌人得实现自动寻路。**这里有一个网上搜不到的问题——实时添加障碍物。**

 ## 二、个人遇到的问题

 主要是指导老师说喜欢玩塔防迷宫，所以我们小组做一个类似明日方舟的塔防游戏，不过得加入迷宫元素，就是在宽阔的地图上放置干员来决定怪物的走向。
 使用Astart Pathfinding project插件，前期我很方便的实现了让敌人自动寻路到指定的地点。但令人头疼的是干员(=防守人员)实时放置到地图中的时候，正在行进的怪物不会避让。也就是Astart算法只在开始的时候扫描了一遍地图中的网格，以后就没有实时扫描来监测和生成新的网格。

 ## 三、解决实时添加障碍物的办法

 最后在A* Pathfinding Project官方网站上看文档才想到解决方案。
*当你在B站上看教程，把Astart算法运用到你的项目后，你想实现实时添加障碍物的功能时，你需要用下面一条语句：*

```javascript
AstarPath.active.Scan();

```

这条语句的作用是：**重新计算所有的图(You can recalculate all graphs)**
将这条语句放在你实现**往地图中添加障碍物**功能的脚本中，具体位置应该是你在实例化一个障碍物的后面加上这一条语句。
以下是我们的项目中实现实时扫描图的：

```javascript
if (canPlaceMonster()
{ 
    monster = (GameObject)Instantiate(GameManagerBehavior.Instance.ClickedBtn.TowerPrefab, transform.position, Quaternion.identity);
    AstarPath.active.Scan();//实时更新扫描网格，使得可以实时添加障碍物
    AudioSource audioSource = gameObject.GetComponent<AudioSource>();
    audioSource.PlayOneShot(audioSource.clip);
    Hover.Instance.Deactivate();
    GameManagerBehavior.Instance.BuyMonster();
    gameManager.Gold -= monster.GetComponent<MonsterData>().CurrentLevel.cost;
 }
```

只添加做注释的那条语句，然后你可以开始运行你的项目，随时向地图添加障碍物，敌人会实时的避开你放置的障碍物。
**运用这些原理你可以做一个迷宫类的塔防，还可以让玩家先搭建一个地图然后开始塔防游戏**。
**如果想知道我们项目的全部内容或者添加A*插件的步骤，就看点赞的
