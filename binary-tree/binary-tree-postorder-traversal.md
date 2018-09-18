# Binary Tree Postorder Traversal

Given a binary tree, return the _postorder_ traversal of its nodes' values.

**Example:**

```text
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [3,2,1]
```

**Follow up:** Recursive solution is trivial, could you do it iteratively?

后序遍历： 左  右 根。 递归解法：

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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) return res;
        helper(res, root);
        return res;
    }
    
    public void helper(List<Integer> res, TreeNode root)
    {
        if(root == null) return;
        helper(res, root.left);
        helper(res, root.right);
        res.add(root.val);
    }
}
```

迭代解法 利用linkedlist 的addfirst方法， 反其道而行之， 从根， 右 左的顺序， 最后由于addFirst是从最后的元素往前加的 所以刚好得到正确答案： 

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
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> res = new LinkedList<>();
        if(root == null) return res;
        Stack<TreeNode> s = new Stack<>();
        s.push(root);
        while(!s.isEmpty())
        {
            TreeNode cur = s.pop();
            res.addFirst(cur.val);
            if(cur.left != null)
                s.push(cur.left);
            if(cur.right != null)
                s.push(cur.right);
        }
        
        return res;
    }
}
```

