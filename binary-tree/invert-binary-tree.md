# Invert Binary Tree



Invert a binary tree.

**Example:**

Input:

```text
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

Output:

```text
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

DFS 递归解法：

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
    // recursion
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return null;
        TreeNode left, right;
        left = root.left;
        right = root.right;
        root.left = invertTree(right);
        root.right = invertTree(left);
        return root;
    }
}
```

DFS stack 迭代解法：

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
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return null;
        Stack<TreeNode> s = new Stack<>();
        s.push(root);
        while(!s.isEmpty())
        {
            TreeNode cur = s.pop();
            TreeNode left = cur.left;
            cur.left = cur.right;
            cur.right = left;
            if(cur.left != null)
                s.push(cur.left);
            if(cur.right != null)
                s.push(cur.right);
        }
        return root;
    }
}
```

BFS 解法， 把stack 换成queue即可

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
    public TreeNode invertTree(TreeNode root) {
        if(root == null) return null;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty())
        {
            TreeNode cur = queue.poll();
            TreeNode left = cur.left;
            cur.left = cur.right;
            cur.right = left;
            if(cur.left != null)
                queue.offer(cur.left);
            if(cur.right != null)
                queue.offer(cur.right);
        }
        return root;
    }
}
```

