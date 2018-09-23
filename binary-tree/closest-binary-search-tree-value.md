# Closest Binary Search Tree Value

#### Description

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

* Given target value is a floating point.
* You are guaranteed to have only one unique value in the BST that is closest to the target.

Have you met this question in a real interview?  YesProblem Correction

#### Example

Given root = `{1}`, target = `4.428571`, return `1`.

算法很简单，求出 lowerBound 和 upperBound。即 &lt; target 的最大值和 &gt;= target 的最小值。  
然后在两者之中去比较谁更接近，然后返回即可。

时间复杂度为 O\(h\)O\(h\)，注意如果你使用 in-order traversal 的化，时间复杂度会是 o\(n\)o\(n\) 并不是最优的。另外复杂度也不是 O\(logn\)O\(logn\) 因为BST 并不保证树高是 logn 的。



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
     * @param root: the given BST
     * @param target: the given target
     * @return: the value in the BST that is closest to the target
     */
    public int closestValue(TreeNode root, double target) {
        // write your code here
        if(root == null) return 0;
        
        TreeNode low = lowerBound(root, target);
        TreeNode upper = upperBound(root, target);
        
        if(low == null) return upper.val;
        if(upper == null) return low.val;
        
        System.out.println("low " + low.val + " upper " + upper.val);
        if(target - low.val <= upper.val - target)
        return low.val;
        else
        return upper.val;
    }
    
    public TreeNode lowerBound(TreeNode root, double target)
    {
        if(root == null) return null;
        if(target <= root.val)
        return lowerBound(root.left, target);
        
        TreeNode lowerNode = lowerBound(root.right, target);
        if(lowerNode != null)
        return lowerNode;
        
        return root;
    }
    
    public TreeNode upperBound(TreeNode root, double target)
    {
        if(root == null) return null;
        
        if(target > root.val)
        return upperBound(root.right, target);
        
        TreeNode upperNode = upperBound(root.left, target);
        if(upperNode != null)
        return upperNode;
        
        return root;
    }
}
```

