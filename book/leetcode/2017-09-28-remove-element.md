
## Question

Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:

```
Given input array nums = [3,2,2,3], val = 3

Your function should return length = 2, with the first two elements of nums being 2.
```

## Solution

定义 `m` 和 `i`，`m` 记录数组中需要修改的位置。比较给定值 `val` 和 `i` 处的值是否相等，相等则将 `i` 向右移动一位；不相等则将 `i` 处的值移动到 `m`处， `m` 和 `i` 均向右移动一位。

```
    public  int solution(int[] nums, int val) {
        int m = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[m] = nums[i];
                m++;
            }
        }
        return m;
    }
```

> Time complextiy: O(n)，一次遍历即可
>
> Space complexity : O(1)
