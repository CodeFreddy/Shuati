# Inorder Successor in BST

#### Description

Given a binary search tree \([See Definition](http://www.lintcode.com/problem/validate-binary-search-tree/)\) and a node in it, find the in-order successor of that node in the BST.

If the given node has no in-order successor in the tree, return `null`.

It's guaranteed _p_ is one node in the given tree. \(You can directly compare the memory address to find p\)Have you met this question in a real interview?  YesProblem Correction

#### Example

Given tree = `[2,1]` and node = `1`:

```text
  2
 /
1
```

return node `2`.

Given tree = `[2,1,3]` and node = `2`:

```text
  2
 / \
1   3
```

return node `3`.

#### Challenge

O\(h\), where h is the height of the BST.



解题思路：

首先先要明确bst的successor的概念， 参考：[https://www.cnblogs.com/Renyi-Fan/p/8252227.html](https://www.cnblogs.com/Renyi-Fan/p/8252227.html)  前驱结点：节点val值小于该节点val值并且值最大的节点  后继节点：节点val值大于该节点val值并且值最小的节点。

代码如下：

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


public class Solution {
    /*
     * @param root: The root of the BST.
     * @param p: You need find the successor node of p.
     * @return: Successor of p.
     */
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        // write your code here
        TreeNode successor = null;
        while(root != null && root.val != p.val)
        {
            if(root.val > p.val)
            {
                successor = root;
                root = root.left;
            }else
            {
                root = root.right;
            }
        }
        
        if(root == null)
        return null;
        
        if(root.right ==null)
        return successor;
        
        root = root.right;
        while(root.left != null)
        {
            root = root.left;
        }
        
        return root;
    }
}
```



