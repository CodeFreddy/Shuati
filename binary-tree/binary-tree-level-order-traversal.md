# Binary Tree Level Order Traversal



Given a binary tree, return the level order traversal of its nodes' values. \(ie, from left to right, level by level\).

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,  


```text
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:  


```text
[
  [3],
  [9,20],
  [15,7]
]
```

这道题一看按层来找node，马上想到bfs，因此用queue就解决问题了。

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for(int i = 0; i < size; i++)
            {
                TreeNode cur = queue.poll();
                list.add(cur.val);
                if(cur.left != null) queue.offer(cur.left);
                if(cur.right != null) queue.offer(cur.right);
            }
            res.add(new ArrayList<>(list));
        }
        
        return res;
    }
}
```

DFS:

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        if(root == null) return res;
        helper(res, root, 0);
        return res;
    }
    
    public void helper(List<List<Integer>> res, TreeNode root, int height)
    {
        if(root == null)
            return;
        if(height >= res.size())
        {
            res.add(new LinkedList<>());
        }
        
        res.get(height).add(root.val);
        helper(res, root.left, height+1);
        helper(res, root.right, height + 1);
        
    }
}
```

