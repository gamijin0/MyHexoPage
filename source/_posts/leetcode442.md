---
title: leetcode442
date: 2017-05-23 19:56:32
tags: algorithms
---

leetcode 第442题
======

题目链接：[Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/#/description)

***

>题目描述：给一个包含 `n` 个数的数组 `a`，其中有的出现两次，有的出现一次，而且所有的数都满足 `1 <= a[i] <= n`，目标：找出所有出现重复的数，要求：不使用额外空间，时间复杂度 `O(n)`


乍一看感觉需要先排序，然后遍历，然后想到  _计数排序_ 这类排序方法的思想：_把对应元素放到对应位置上_

***
于是有一个解决方法：

1. 一个指针指向起始位置
2. 若这个指针指向的数字与其索引不相符合 且 这个数字不是 `-1` 时，_尝试_ 将这个数字与这个数字对应的索引地址上的数交换，否则指针向前
3. 若待交换时两个数相同，则说明出现了重复的数，_交换失败_，此时记录下这个数，在此时指针处标记 `-1` ，指针继续向前
4. 若交换成功，则指针不移动，重复 `步骤1`
5. 若指针到达数组尾部，结束

***

###流程图如下

```flow

init=>start: i=0,res=[ ]
isExist=>condition: nums[i]-1 == i 
&& 
nums[i] != -1
swap=>operation: 交换 nums[i] 与 nums[ nums[i]-1 ]
go=>operation: i += 1
finish=>condition: i > len(nums)
sameNum=>condition: 判断是否重复:
nums[ nums[i]-1 ] ==
nums[i]
sameOperation=>operation: 出现重复数字,
将nums[ nums[i]-1 ]保存在res中,
nums[i]=-1


ex=>end: 返回res

init->isExist
isExist(yes)->sameNum
isExist(no,right)->go(right)->finish(no)->isExist
finish(no,right)->isExist
finish(yes)->ex
sameNum(yes,right)->sameOperation->go
sameNum(no)->swap-go

```



***

Python代码如下：

```python


class Solution(object):
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        i=0
        res = []
        while(i<len(nums)):
            if(nums[i]!=-1 and nums[i] != i+1):
                temp = nums[nums[i]-1]
                if(nums[i]==temp):
                    res.append(temp)
                    nums[i]=-1
                else:
                    nums[nums[i]-1] = nums[i]
                    nums[i] = temp
                    continue
            i += 1

        return res


```              
