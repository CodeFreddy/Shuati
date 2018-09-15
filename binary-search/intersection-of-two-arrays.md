# Intersection of Two Arrays



Given two arrays, write a function to compute their intersection.

**Example 1:**

```text
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]
```

**Example 2:**

```text
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
```

**Note:**

* Each element in the result must be unique.
* The result can be in any order.

解法1：O\(N\) 挨个遍历数组。

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        //O(n) solution
        Set<Integer> set = new HashSet<>();
        Set<Integer> temp = new HashSet<>();
        for(int i = 0; i < nums1.length; i++)
        {
            set.add(nums1[i]);
        }
        
        for(int i = 0; i < nums2.length; i++)
        {
            if(set.contains(nums2[i]))
                temp.add(nums2[i]);
        }
        int[] result = new int[temp.size()];
        int j = 0;
        for(Integer num: temp)
        {
            result[j++] = num;
        }
        return result;
    }
}
```

解法2： O\(nlogn\) 利用Arrays 的排序， 然后挨个比对。Arrays的排序有两种， 一种是合并排序， 时间复杂度是O\(nlogn\), 比较稳定。另一种是快速排序，快速排序是不稳定的， 时间复杂度为O（nlogn），最坏情况下是O\(n^2\)。

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0;
        int j = 0;
        while(i < nums1.length && j < nums2.length)
        {
            if(nums1[i] < nums2[j])
                i++;
            else if(nums1[i] > nums2[j])
                j++;
            else
            {
                set.add(nums1[i]);
                i++;
                j++;    
            }
        }
        
        int[] result = new int[set.size()];
        int k = 0;
        for(Integer num: set)
        {
            result[k++] = num;
        }
        
        return result;
    }
}
```

解法3：O\(nlogn\) binary search:

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
       Set<Integer> set = new HashSet<>();
        Arrays.sort(nums2);
        for(Integer num: nums1)
        {
            if(BinarySearch(nums2, num))
                set.add(num);
        }
        int[] result = new int[set.size()];
        int i = 0;
        for(Integer num: set)
        {
            result[i++] = num;
        }
        return result;
    }
    
    public boolean BinarySearch(int[] nums2, int num)
    {
        if(nums2 == null || nums2.length == 0)
            return false;
        int start = 0, end = nums2.length - 1;
        while(start + 1 < end)
        {
            int mid = start + (end - start) / 2;
            if(nums2[mid] == num) return true;
            if(nums2[mid] < num)
            {
                start = mid;
            }else if(nums2[mid] > num)
            {
                end = mid;
            }
        }
        if(nums2[start] == num) return true;
        if(nums2[end] == num) return true;
        return false;
    }
}
```



