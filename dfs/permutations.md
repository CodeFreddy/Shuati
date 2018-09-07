# Permutations



Given a collection of **distinct** integers, return all possible permutations.

**Example:**

```text
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

解题思路：这道题就是考察递归，根据题意，每个元素都是不同的， 然后求出所有可能的排列。 首先需要一个curList来存放可能形成的序列， 然后一个boolean类型的数组来存放该位置的元素被访问的状态。没被访问过就是false，否则是true。 递归的过程中每一次都会遍历一次数组。最后在每一层最后要记得重置used的值和删掉curList里那一层的值。这样才不会影响后续的记录。

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        DFS(res, new boolean[nums.length], new LinkedList<Integer>(), nums);
        return res;
    }
    
    public void DFS(List<List<Integer>> res, boolean[] used, List<Integer> curList, int[] nums)
    {
        if(curList.size() == nums.length)
            res.add(new LinkedList(curList));
        else
        {
            for(int i = 0; i < nums.length; i++)
            {
                if(used[i] == false)
                {
                    curList.add(nums[i]);
                    used[i] = true;
                    DFS(res, used, curList, nums);
                    curList.remove(curList.size() - 1);
                    used[i] = false;
                }
            }
        }
    }
}
```

