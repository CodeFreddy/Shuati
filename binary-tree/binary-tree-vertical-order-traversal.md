# Binary Tree Vertical Order Traversal

#### Description

Given a binary tree, return the vertical order traversal of its nodes' values. \(ie, from top to bottom, column by column\).

If two nodes are in the same row and column, the order should be from **left to right**.Have you met this question in a real interview?  YesProblem Correction

#### Example

Given binary tree `{3,9,20,#,#,15,7}`

```text
   3
  /\
 /  \
 9  20
    /\
   /  \
  15   7
```

Return its vertical order traversal as:  
`[[9],[3,15],[20],[7]]`

Given binary tree `{3,9,8,4,0,1,7}`

```text
     3
    /\
   /  \
   9   8
  /\  /\
 /  \/  \
 4  01   7
```

Return its vertical order traversal as:  
`[[4],[9],[3,0,1],[8],[7]]`

利用bfs遍历bst， 然后增添一个queue 存放col， 再用一个map来存放每一列的列表。

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: the root of tree
     * @return: the vertical order traversal
     */
    public List<List<Integer>> verticalOrder(TreeNode root) {
        // write your code here
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<TreeNode> queue = new LinkedList<>();
        Queue<Integer> qcol = new LinkedList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        queue.offer(root);
        qcol.offer(0);
        
        while(!queue.isEmpty())
        {
            TreeNode cur = queue.poll();
            int col = qcol.poll();
            if(!map.containsKey(col))
            {
                map.put(col, new ArrayList<>(Arrays.asList(cur.val)));
            }else
            map.get(col).add(cur.val);
            
            if(cur.left != null)
            {
                queue.offer(cur.left);
                qcol.offer(col - 1);
                
            }
            
            if(cur.right != null)
            {
                queue.offer(cur.right);
                qcol.offer(col + 1);
            }
            
        }
        
       for(int i = Collections.min(map.keySet()); i <= Collections.max(map.keySet()); i++)
       {
           res.add(map.get(i));
       }
        
        return res;
    }
}
```

