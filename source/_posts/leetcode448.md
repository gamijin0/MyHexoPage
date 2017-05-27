---
title: leetcode448
date: 2017-05-24 12:35:50
tags: algorithms
---


Leetcode 第448题
-------

题目链接： [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/#/description)

题目描述：

>Given an array of integers where `1 ≤ a[i] ≤ n (n = size of array)`, some elements appear twice and others appear once.

>Find all the elements of `[1, n]` inclusive that do not appear in this array.

>Could you do it without extra space and in `O(n)` runtime? You may assume the returned list does not count as extra space.
                                                              
题目很简单，和[442题](/2017/05/23/leetcode442/)几乎一样

代码如下：

```python
class Solution(object):
    def findDisappearedNumbers(self, nums):
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
                    nums[i]=-1
                else:
                    nums[nums[i]-1] = nums[i]
                    nums[i] = temp
                    continue
            i += 1

        for i,v in enumerate(nums):
            if(v==-1):
                res.append(i+1)

        return res


```
