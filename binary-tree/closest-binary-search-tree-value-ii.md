# Closest Binary Search Tree Value II

#### Description

Given a non-empty binary search tree and a target value, find `k` values in the BST that are closest to the target.

* Given target value is a floating point.
* You may assume `k` is always valid, that is: `k ≤ total` nodes.
* You are guaranteed to have only one `unique` set of k values in the BST that are closest to the target.

Have you met this question in a real interview?  YesProblem Correction

#### Example

Given root = `{1}`, target = `0.000000`, k = `1`, return `[1]`.

#### Challenge

Assume that the BST is balanced, could you solve it in less than O\(n\) runtime \(where n = total nodes\)?

解法1：



暴力方法。时间复杂度 O\(n\)O\(n\)，空间复杂度也是 O\(n\)O\(n\)

* 先用 inorder traversal 求出中序遍历
* 找到第一个 &gt;= target 的位置 index
* 从 index-1 和 index 出发，设置两根指针一左一右，获得最近的 k 个整数

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
     * @param k: the given k
     * @return: k values in the BST that are closest to the target
     */
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        // write your code here
        List<Integer> values = new ArrayList<>();
        List<Integer> res = new ArrayList<>();
        if(k == 0 || root == null)
        return res;
        
        traverse(root, values);
        
        int i = 0, n = values.size();
        for(; i < n; i++)
        {
            if(values.get(i) >= target)
            {
                break;
            }
        }
        
        if(i >= n)
        return values.subList(n - k, n);
        
        int left = i - 1, right = i;
        
        for(int j = 0; j < k; j++)
        {
            if(left >= 0 && (right >= n || target - values.get(left) < values.get(right) - target))
            {
                res.add(values.get(left));
                left--;
            }else{
                res.add(values.get(right));
                right++;
            }
        }
        return res;
        
    }
    
    public void traverse(TreeNode root, List<Integer> values)
    {
        if(root == null) return;
        
        traverse(root.left, values);
        values.add(root.val);
        traverse(root.right, values);
        
    }
}
```

最优算法，时间复杂度 O\(k + logn\)，空间复杂度 O\(logn\)

实现如下的子函数：

1. getStack\(\) =&gt; 在假装插入 target 的时候，看看一路走过的节点都是哪些，放到 stack 里，用于 iterate
2. moveUpper\(stack\) =&gt; 根据 stack，挪动到 next node
3. moveLower\(stack\) =&gt; 根据 stack, 挪动到 prev node

有了这些函数之后，就可以把整个树当作一个数组一样来处理，只不过每次 i++ 的时候要用 moveUpper，i--的时候要用 moveLower



（并不理解为什么时间复杂度是O\(k + logn\), 如果考虑到最坏的情况 moveupper和movelower 可能在while循环里面都会花很长时间来遍历）

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
     * @param k: the given k
     * @return: k values in the BST that are closest to the target
     */
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        // write your code here
        List<Integer> values = new ArrayList<>();
        if(root == null || k == 0) return values;
        
        Stack<TreeNode> lowerStack = new Stack<>();
        Stack<TreeNode> upperStack = new Stack<>();
        lowerStack = getStack(root, target);
        upperStack.addAll(lowerStack);
        
        if(target < lowerStack.peek().val)
        {
            moveLower(lowerStack);
            
        }else
            moveUpper(upperStack);
        
        for(int i = 0; i < k; i++)
        {
            if(lowerStack.isEmpty() || ( !upperStack.isEmpty() &&target - lowerStack.peek().val > upperStack.peek().val - target))
            {
                values.add(upperStack.peek().val);
                moveUpper(upperStack);
            }else
                {
                    values.add(lowerStack.peek().val);
                    moveLower(lowerStack);
                }
        }
        
        return values;
    }
    
    public Stack<TreeNode> getStack(TreeNode root, double target)
    {
        Stack<TreeNode> s = new Stack<>();
        while(root != null)
        {
            s.push(root);
            if(target < root.val)
            root = root.left;
            else
            root = root.right;
        }
        return s;
    }
    
    public void moveUpper(Stack<TreeNode> upperStack)
    {
        TreeNode node = upperStack.peek();
        if(node.right == null)
        {
            node = upperStack.pop();
            while(!upperStack.isEmpty() && upperStack.peek().right == node)
            {
                node = upperStack.pop();
                
            }
            return;
        }
        
        node = node.right;
        while(node != null)
        {
            upperStack.push(node);
            node = node.left;
        }
        
    }
    
    public void moveLower(Stack<TreeNode> lowerStack)
    {
        TreeNode node = lowerStack.peek();
        if(node.left == null)
        {
            node = lowerStack.pop();
            while(!lowerStack.isEmpty() && lowerStack.peek().left == node)
            {
                node = lowerStack.pop();
            }
            return;
        }
        
        node = node.left;
        while(node != null)
        {
            lowerStack.push(node);
            node = node.right;
        }
    }
}
```

