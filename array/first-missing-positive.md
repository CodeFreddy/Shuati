# First Missing Positive

Given an unsorted integer array, find the smallest missing positive integer.

**Example 1:**

```text
Input: [1,2,0]
Output: 3
```

**Example 2:**

```text
Input: [3,4,-1,1]
Output: 2
```

**Example 3:**

```text
Input: [7,8,9,11,12]
Output: 1
```

**Note:**

Your algorithm should run in _O_\(_n_\) time and uses constant extra space.

解题思路：

这道题首先要知道题目需要寻找的是第一个missing的正整数。0不是正整数，负数自然也不是，还有一个需要注意的是array里的元素得小于等于nums.length。 比如\[ 99, 99, 100 \]里 需要返回的是1。 因为是从1，2，3，4这样开始的。 1是第一个missing的正整数。因此需要遍历一遍array，把符合要求的数字放到他们本来应该在的位置上。比如\[ 3, 1, 4, -1\] 最后要变成 \[ 1, -1, 3, 4 \]。 这样就可以很容易发现是2 missing了。

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        for(int i = 0; i < nums.length; i++)
        {
            while(nums[i] > 0 && nums[i] <= nums.length && nums[i] != nums[nums[i] - 1])
            {
                int temp = nums[nums[i] - 1];
                nums[nums[i] - 1] = nums[i];
                nums[i] = temp;
            }
        }
        
        for(int i = 0; i < nums.length; i++)
        {
            if(nums[i] != i + 1)
                return i + 1;
        }
        
        return nums.length + 1;
    }
}
```

 

