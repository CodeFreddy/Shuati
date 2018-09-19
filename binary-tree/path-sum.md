# Path Sum

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note:** A leaf is a node with no children.

**Example:**

Given the below binary tree and `sum = 22`,

```text
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.

递归解法：

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
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null) return false;
        if(root.left == null && root.right == null && sum - root.val == 0) return true;
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```

DFS 迭代实现：

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
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null) return false;
        Stack<TreeNode> s = new Stack<>();
        Stack<Integer> value = new Stack<>();
        s.push(root);
        value.push(sum);
        while(!s.isEmpty() && !value.isEmpty())
        {
            TreeNode cur = s.pop();
            int top = value.pop();
            if(cur.left == null && cur.right == null && top - cur.val == 0) return true;
            if(cur.right != null)
            {
                s.push(cur.right);
                value.push(top - cur.val);
                
            }
            if(cur.left != null)
            {
                s.push(cur.left);
                value.push(top - cur.val);
            }
        }
        return false;
    }
}
```

