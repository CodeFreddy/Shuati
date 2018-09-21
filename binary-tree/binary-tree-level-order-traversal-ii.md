# Binary Tree Level Order Traversal II



Given a binary tree, return the bottom-up level order traversal of its nodes' values. \(ie, from left to right, level by level from leaf to root\).

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,  


```text
    3
   / \
  9  20
    /  \
   15   7
```

return its bottom-up level order traversal as:  


```text
[
  [15,7],
  [9,20],
  [3]
]
```

BFS:

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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        if(root == null) return res;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty())
        {
            int size = queue.size();
            List<Integer> sublist = new LinkedList<>();
            for(int i = 0; i < size; i++)
            {
                TreeNode cur = queue.poll();
                sublist.add(cur.val);
                if(cur.left != null) queue.offer(cur.left);
                if(cur.right != null) queue.offer(cur.right);
                
            }
            res.add(0, new LinkedList<>(sublist));
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
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        if(root == null) return res;
        helper(res, 0, root);
        return res;
        
    }
    
    public void helper(List<List<Integer>> res, int level, TreeNode root)
    {
        if(root == null) return;
        if(level >= res.size()) res.add(0,new LinkedList<>());
        
        
        helper(res, level + 1, root.left);
        helper(res, level + 1, root.right);
        res.get(res.size() - 1 -level).add(root.val);
    }
}
```

