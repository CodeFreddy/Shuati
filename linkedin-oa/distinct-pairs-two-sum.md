# Distinct Pairs, two sum

In this challenge, you will be given an array of integers and a target value. Determine the number of distinct pairs of elements in the array that sum to the target value. Two pairs \(a, b\) and \(c, d\) are considered to be distinct if and only if the values in sorted order do not match, i.e., \(1, 9\) and \(9, 1\) are indistinct but \(1, 9\) and \(9, 2\) are distinct. For instance, given the array \[1, 2, 3, 6, 7, 8, 9, 1\], and a target value of 10, the seven pairs \(1,9\), \(2,8\), \(3,7\), \(8, 2\), \(9, 1\), \(9, 1\), and \(1, 9\) all sum to 10 and only three distinct pairs: \(1, 9\), \(2, 8\), and \(3, 7\). Function Description Complete the function numberOfPairs in the editor below. The function must return an integer, the total number of distinct pairs of elements in the array that sum to the target value.

```java
 static int distinctPairs(int[] nums, int target)
    {
        Set<Integer> starters = new HashSet<Integer>();
        Set<Integer> uniqs = new HashSet<Integer>();

        for(int i = 0; i < nums.length; i++)
        {
            if(uniqs.contains(target - nums[i]))
            {
                if(!starters.contains(nums[i]))
                {
                    starters.add(target - nums[i]);
                }
            }
            uniqs.add(nums[i]);
        }
        return starters.size();
    }



    public static void main(String[] args)
    {
        int[] a = new int[]{6,6,3,9,3,5,1};
        int target = 12;
        int result = distinctPairs(a, target);
        System.out.println("result: " + result);
    }
```

