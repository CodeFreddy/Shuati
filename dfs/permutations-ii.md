# Permutations II



#### Description

Given a list of numbers with duplicate number in it. Find all **unique** permutations.Have you met this question in a real interview?  Yes

#### Example

For numbers `[1,2,2]` the unique permutations are:

```text
[
  [1,2,2],
  [2,1,2],
  [2,2,1]
]
```

解题思路：这道题和permutation I 唯一的不同是可能出现重复元素。 那在做循环遍历元素时，设置一个变量，储存前一个元素的值。如果与当前元素相同的元素被取用过，那么与之相同的所有元素都要跳过。

 举个例子：对于序列&lt;1,1,2,3&gt;。在DFS首遍历时，1 作为首元素被加到list中，并进行后续元素的添加；那么，当DFS跑完第一个分支，遍历到1 \(第二个\)时，这个1 不再作为首元素添加到list中，因为1 作为首元素的情况已经在第一个分支中考虑过了。

另外，需要在执行DFS之前把数组排序一遍， 这样才能很好的判断当前值是否和前一个元素的值一样。

```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        Arrays.sort(nums);
        DFS(res, new boolean[nums.length], new LinkedList<Integer>(), nums);
        return res;
    }
    
    public void DFS(List<List<Integer>> res, boolean[] used, List<Integer> curList, int[] nums)
    {
        if(curList.size() == nums.length)
            res.add(new LinkedList(curList));
        else{
            int preNum = nums[0] - 1;
            for(int i = 0; i < nums.length; i++)
            {
                if(used[i] == false && nums[i] != preNum)
                {
                    preNum = nums[i];
                    used[i] = true;
                    curList.add(nums[i]);
                    DFS(res, used, curList, nums);
                    used[i] = false;
                    curList.remove(curList.size() - 1);
                }
            }
        }
    }
}
```

