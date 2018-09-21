# Binary Tree Zigzag Level Order Traversal



Given a binary tree, return the zigzag level order traversal of its nodes' values. \(ie, from left to right, then right to left for the next level and alternate between\).

For example:  
Given binary tree `[3,9,20,null,null,15,7]`,  


```text
    3
   / \
  9  20
    /  \
   15   7
```

return its zigzag level order traversal as:  


```text
[
  [3],
  [20,9],
  [15,7]
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        if(root == null) return res;
        Queue<TreeNode> queue = new LinkedList<>();
        int count = 0;
        queue.offer(root);
        
        while(!queue.isEmpty())
        {
            int size = queue.size();
            List<Integer> sublist = new LinkedList<>();
            for(int i = 0; i < size; i++)
            {
                TreeNode cur = queue.poll();
                if(count % 2 == 0)
                {
                    sublist.add(cur.val);
                }else
                    sublist.add(0, cur.val);
                if(cur.left != null)
                    queue.offer(cur.left);
                if(cur.right != null)
                    queue.offer(cur.right);
            }
            count++;
            res.add(new LinkedList<>(sublist));
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<>();
        helper(res, 0, 0, root);
        return res;
    }
    
    public void helper(List<List<Integer>> res, int level, int count, TreeNode root)
    {
        if(root == null) return;
        if(res.size() <= level) res.add(new LinkedList<>());
        helper(res, level + 1, count + 1, root.left);
        helper(res, level + 1, count + 1, root.right);
        if(count % 2 == 0)
        {
            res.get(level).add(root.val);
        }else
            res.get(level).add(0, root.val);
    }
}
```

