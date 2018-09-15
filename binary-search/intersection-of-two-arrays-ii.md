# Intersection of Two Arrays II



Given two arrays, write a function to compute their intersection.

**Example 1:**

```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]
```

**Example 2:**

```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]
```

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

**Follow up:**

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

解法一： 和版本1一样， 直接遍历两个数组， 找到相同的元素，这是最直接的暴力解法。

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        List<Integer> temp = new ArrayList<>();
        int i = 0, j = 0;
        while(i < nums1.length && j < nums2.length)
        {
            if(nums1[i] < nums2[j])
                i++;
            else if(nums1[i] > nums2[j])
                j++;
            else
            {
                temp.add(nums1[i]);
                i++;
                j++;
            }
        }
        int[] result = new int[temp.size()];
        int k = 0;
        for(Integer num : temp)
        {
            result[k++] = num;
        }
        
        return result;
    }
}
```

