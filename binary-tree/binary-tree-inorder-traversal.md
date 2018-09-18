# Binary Tree Inorder Traversal

Given a binary tree, return the _inorder_ traversal of its nodes' values.

**Example:**

```text
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?

中序遍历顺序： 左， 中， 右。 首先先用递归解：

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
    // recursion solution
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) return res;
        helper(res, root);
        return res;
    }
    
    public void helper(List<Integer> res, TreeNode root)
    {
        if(root == null) return;
        helper(res, root.left);
        res.add(root.val);
        helper(res, root.right);
    }
}
```

然后是迭代解法：

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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<Integer>();
        if(root == null) return res;
        TreeNode cur = root;
        Stack<TreeNode> s = new Stack<>();
        while(cur != null || !s.isEmpty())
        {
            while(cur != null)
            {
                s.push(cur);
                cur = cur.left;
            }
            cur = s.pop();
            res.add(cur.val);
            cur = cur.right;
        }
        
        return res;
    }
    
    
}
```

