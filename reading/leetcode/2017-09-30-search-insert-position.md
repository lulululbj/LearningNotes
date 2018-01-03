
## Question

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.

```
[1,3,5,6], 5 → 2
[1,3,5,6], 2 → 1
[1,3,5,6], 7 → 4
[1,3,5,6], 0 → 0
```

给定已排序数组和目标值。
目标值在数组中已存在直接返回下标。
若不存在，将目标值插入数组返回下标。

## Solution

### 循环

由于数组已排序，直接循环判断。

```
public int solution(int[] nums, int target) {
    for (int i = 1; i <= nums.length - 1; i++) {
        if (target == nums[i]) return i;
        if (target > nums[i - 1] && target < nums[i]) return i;
    }

    if (target > nums[nums.length - 1]) return nums.length;
    else return 0;
}
```

> Time complextiy: O(n)
>
> Space complexity : O(1)

### 二分法

有序集合可以用经典的二分法查找。

```
public int solution(int[] nums, int target) {
    int start = 0;
    int end = nums.length - 1;
    while (start <= end) {
        int middle = (start + end) / 2;
        if (target == nums[middle]) return middle;
        if (target > nums[middle]) start = middle + 1;
        else end = middle - 1;
    }
    return start;
}
```

> Time complextiy: O($log~2 n$)
>
> Space complexity : O(1)
