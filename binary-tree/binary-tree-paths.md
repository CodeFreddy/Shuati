# Binary Tree Paths



Given a binary tree, return all root-to-leaf paths.

**Note:** A leaf is a node with no children.

**Example:**

```text
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> ans = new ArrayList<>();
        if(root == null) return ans;
        searchPath(ans, "", root);
        return ans;
    }
    
    public void searchPath(List<String> ans, String path, TreeNode root)
    {
        if(root.left == null && root.right == null) ans.add(path + root.val);
        if(root.left != null) searchPath(ans, path + root.val + "->", root.left);
        if(root.right != null) searchPath(ans, path + root.val + "->", root.right);
    }
}
```

BFS 解法：

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
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> ans = new ArrayList<>();
        if(root == null) return ans;
        Queue<String> str = new LinkedList<>();
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        str.offer("");
        while(!queue.isEmpty())
        {
            TreeNode curNode = queue.poll();
            String curStr = str.poll();
            if(curNode.left == null && curNode.right == null) ans.add(curStr + curNode.val);
            if(curNode.left != null)
            {
                queue.offer(curNode.left);
                str.offer(curStr + curNode.val + "->");
                
            }
            
            if(curNode.right != null)
            {
                queue.offer(curNode.right);
                str.offer(curStr + curNode.val + "->");
            }
        }
        return ans;
    }
}
```

