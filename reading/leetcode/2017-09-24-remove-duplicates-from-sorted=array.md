---
layout: post
title: "LeetCode - Remove Duplicates from Sorted Array"
author: luyao
categories: LeetCode
tags: Array Easy
excerpt: ""
---

* content
{:toc}

## Question

Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

For example,

```
Given input array nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.
```

返回已排序数组中不重复的元素个数，要求：
* 不能再创建数组，只能已有空间
* 若返回个数 k，则代表数组前 k 个元素互不重复

## Solution

从第一个元素开始依次与之后的元素比较，大小不一样时，将后面的元素值赋给当前元素的下一个元素。并从下一个元素开始重复上述步骤。每次出现不一样的情况时计数，即代表不重复元素的个数。

```
public static int solution(int[] nums) {
    int m = 0;
    for (int i = 1; i < nums.length; i++) {
        if (nums[m] != nums[i]) {
            m++;
            nums[m] = nums[i];
        }
    }
    return m + 1;  
}
```

> Time complextiy: O(n)，一次遍历即可
>
> Space complexity : O(1)
