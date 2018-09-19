# Path Sum II



Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

**Note:** A leaf is a node with no children.

**Example:**

Given the below binary tree and `sum = 22`,

```text
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```

Return:

```text
[
   [5,4,11,2],
   [5,8,4,5]
]
```

递归解法:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> ans = new LinkedList<>();
        List<Integer> curList = new LinkedList<>();
        if(root == null) return ans;
        helper(ans, curList, root, sum);
        return ans;
        
    }
    
    public void helper(List<List<Integer>> ans, List<Integer> curList, TreeNode root, int sum)
    {
        if(root == null) return;
        curList.add(root.val);
        if(root.left == null && root.right == null && sum - root.val == 0)
        {
            ans.add(new LinkedList<>(curList));
            curList.remove(curList.size() - 1);
            return;
        }else
        {
            helper(ans, curList, root.left, sum - root.val);
            helper(ans, curList, root.right, sum - root.val);
        }
        curList.remove(curList.size() - 1);
    }
}
```

