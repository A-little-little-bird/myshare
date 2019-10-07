---
title: 查找树中节点的编号
comments: true
date: 2019-06-08 11:11:53
tags: 树
categories: 实际问题
---

### 问题描述

>给定一棵树，树中各节点的默认编号按照深度优先遍历排序。现给定一节点数组，请返回这组节点所对应的编号数组。
>
>例如：

```
      8                           对应编号:1 2 3 4 5 6 7  
    /   \           如左图，各节点按序访问为:[8,5,2,4,7,6,9],
   5     7          若给定查询数组为:[7,4],则返回值应该为:[5,4]
  / \   / \
 2   4 6   9
```
### 解决方案
> 暂时以解决问题优先，之后若有新的思路再进行优化。
> 树的深度优先遍历使用递归方式能够简明实现，但问题中需要返回命中节点的序号，因此再遍历的时候还需要加上全局的index，记录节点的访问次序。基本流程如下：
> 1）从目标数组中取出需要查找的节点；
> 2）遍历树开始查找节点位置（假定该节点一定存在此树中）；
> 3）依次遍历树的节点，若节点为空直接返回；
> 4）若节点不为空，则比对值是否相等，相等将序号加入返回数组；
> 5）若不等，判断该节点是否有子树，无直接返回，有则递归，从 3）开始遍历子树；

### 具体代码
```
/**
/* 使用js代码为例（实际需要）
/* 递归查找函数
/* z_tree为树，targetID为查找节点，index为节点编号，select为返回数组
/**
function findIndex(z_tree,targetID,index,select) {
	if(z_tree){
		if(z_tree.ID==targetID){
			select.push(index.count);
		}
		else if(z_tree.child){
			for(var i=0;i<z_tree.child.length;i++){
				index.count++;
				findIndex(z_tree.child[i],targetID,index,select);
			}
		}
	}
};
// 创建树
var z_tree={
	ID:'asd001',
	child:[
		{
			ID:'asd002',
			child:[
				{
					ID:'asd005',
				},
				{
					ID:'asd006',
				}
			]
		},
		{
			ID:'asd003',
			child:[
				{
					ID:'asd007',
				},
				{
					ID:'asd008',
				}
			]
		},
		{
			ID:'asd004',
			child:[
				{
					ID:'asd009',
				},
				{
					ID:'asd010',
				}
			]
		}
	],
}
// 目标节点数组
var targetID=['asd008','asd002'];
// 节点编号（使用对象构建引用类型）
var index={count:1};
// 返回数组
var select=[];
// 开始遍历
for(var i=0;i<targetID.length;i++){
	index.count=1;  // 每次遍历前初始化序号
	findIndex(z_tree,targetID[i],index,select);
}
console.log(select)
```





