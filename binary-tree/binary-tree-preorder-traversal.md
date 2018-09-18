# Binary Tree Preorder Traversal

Given a binary tree, return the _preorder_ traversal of its nodes' values.

**Example:**

```text
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?

先序遍历： 根 左 右。 递归解法：

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer>res = new ArrayList<>();
        if(root == null) return res;
        helper(res, root);
        return res;
        
    }
    public void helper(List<Integer> res, TreeNode root)
    {
        if(root == null) return;
        res.add(root.val);
        helper(res, root.left);
        helper(res, root.right);
    }
}
```

迭代解法：

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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        if(root == null ) return res;
        Stack<TreeNode> s = new Stack<>();
        s.push(root);
        while(!s.isEmpty())
        {
            TreeNode cur = s.pop();
            res.add(cur.val);
            if(cur.right != null) s.push(cur.right);
            if(cur.left != null) s.push(cur.left);
            
        }
        
        return res;
    }
    
}
```

