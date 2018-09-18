# Same Tree



Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

**Example 1:**

```text
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
```

**Example 2:**

```text
Input:     1         1
          /           \
         2             2

        [1,2],     [1,null,2]

Output: false
```

**Example 3:**

```text
Input:     1         1
          / \       / \
         2   1     1   2

        [1,2,1],   [1,1,2]

Output: false
```

利用迭代的preorder来做：

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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null) return true;
        if(p == null || q == null) return false;
        Stack<TreeNode> sp = new Stack<>();
        Stack<TreeNode> sq = new Stack<>();
        TreeNode curp = p;
        TreeNode curq = q;
        while((curp != null && curq != null) || (!sp.isEmpty() && !sq.isEmpty()))
        {
            while(curp != null || curq != null)
            {
                if(curp == null || curq == null || curp.val != curq.val) return false;
                sp.push(curp);
                sq.push(curq);
                curp = curp.left;
                curq = curq.left;
            }
            
            curp = sp.pop();
            curq = sq.pop();
            curp = curp.right;
            curq = curq.right;
        }
        return true;
              
    }
}
```

