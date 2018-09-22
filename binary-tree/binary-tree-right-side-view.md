# Binary Tree Right Side View



Given a binary tree, imagine yourself standing on the _right_ side of it, return the values of the nodes you can see ordered from top to bottom.

**Example:**

```text
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```

解题思路： 利用dfs来做 每次只会在一层选取一个节点，那么遍历到这一层的深度应该和result的size相同才应该加入 否则就说明这一层已经有节点加入了

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
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        helper(res, root, 0);
        return res;
    }
    
    public void helper(List<Integer> res, TreeNode cur, int depth)
    {
        if(cur == null) return;
        if(res.size() == depth)
            res.add(cur.val);
        helper(res, cur.right, depth + 1);
        helper(res, cur.left, depth + 1);
    }
}
```

BFS:

原理也差不多， 只是这边判断条件变成当处理同一层的元素时 第一个出queue的元素就是想寻找的答案， 当然如queue的顺序应该是从右边先开始

```java
public class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        // reverse level traversal
        List<Integer> result = new ArrayList();
        Queue<TreeNode> queue = new LinkedList();
        if (root == null) return result;
        
        queue.offer(root);
        while (queue.size() != 0) {
            int size = queue.size();
            for (int i=0; i<size; i++) {
                TreeNode cur = queue.poll();
                if (i == 0) result.add(cur.val);
                if (cur.right != null) queue.offer(cur.right);
                if (cur.left != null) queue.offer(cur.left);
            }
            
        }
        return result;
    }
}
```

