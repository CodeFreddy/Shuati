# Rotate Array



Given an array, rotate the array to the right by _k_ steps, where _k_ is non-negative.

**Example 1:**

```text
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]
```

**Example 2:**

```text
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
```

解题思路：利用分步的思想，定义一个反转数组的函数，进行三次反转，进而得到目标数组.

* 首先进行原数组的整体反转；
* 将反转后的数组的当前k个元素进行反转；
* 再将后n-k个元素进行反转.

```java
class Solution {
    public void rotate(int[] nums, int k) {
        int n = nums.length;
        k %= n;
        reverse(nums, 0 , n-1);
        reverse(nums, 0, k-1);
        reverse(nums, k, n-1);
    }
    
    public void reverse(int []nums, int start, int end)
    {
        while(start < end)
        {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

* 注意这里反转函数reverse\(\)对数组操作，每次使用首尾一一对应的元素进行反转；
* 旋转数组注意k&gt;n的情况，一旦k=n，则相当于对数组不进行操作，故这里的k=k%n，取余数.

