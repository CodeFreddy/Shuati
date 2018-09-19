# Find Leaves of Binary Tree

#### Description

Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is empty.Have you met this question in a real interview?  YesProblem Correction

#### Example

Given binary tree:

```text
    1
   / \
  2   3
 / \     
4   5    
```

Returns `[[4, 5, 3], [2], [1]]`.

解题思路：

利用dfs 求深度， 然后再理由hashmap， 将具有相同深度的节点放在一起，最后根据深度值，循环提取存放节点的list到ans里面

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */


public class Solution {
    /*
     * @param root: the root of binary tree
     * @return: collect and remove all leaves
     */
    public List<List<Integer>> findLeaves(TreeNode root) {
        // write your code here
        List<List<Integer>> ans = new ArrayList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        int depth = dfs(root, map);
        for(int i = 1; i <= depth; i++)
        {
            ans.add(new ArrayList(map.get(i)));
        }
        return ans;
        
    }
    
    public int dfs(TreeNode cur, Map<Integer, List<Integer>> map)
    {
        if(cur == null)
        return 0;
        
        int d = Math.max(dfs(cur.left, map), dfs(cur.right, map)) + 1;
        map.putIfAbsent(d, new ArrayList<>());
        map.get(d).add(cur.val);
        return d;
    }
}
```

