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

 这道二叉树的之字形层序遍历是之前那道[\[LeetCode\] Binary Tree Level Order Traversal 二叉树层序遍历](http://www.cnblogs.com/grandyang/p/4051321.html)的变形，不同之处在于一行是从左到右遍历，下一行是从右往左遍历，交叉往返的之字形的层序遍历。根据其特点我们用到栈的后进先出的特点，这道题我们维护两个栈，相邻两行分别存到两个栈中，进栈的顺序也不相同，一个栈是先进左子结点然后右子节点，另一个栈是先进右子节点然后左子结点，这样出栈的顺序就是我们想要的之字形了。再设置一个flag变量 根据flag变量来判断是左子节点先开始还是右子节点先开始。 然后每一次再交换一下curlevel和nextlevel的stack， 这样得到的就是想要的结果。



```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    // write your code here
    List<List<Integer>> result = new ArrayList<>();
    if(root == null) return  result;
    Stack<TreeNode> curLevel = new Stack<>();
    Stack<TreeNode> nextLevel = new Stack<>();
    Stack<TreeNode> temp = null;
    boolean flag = true;

    curLevel.push(root);
    while(!curLevel.isEmpty())
    {
        List<Integer> level = new ArrayList<>();

        while(!curLevel.isEmpty())
        {
            TreeNode node = curLevel.pop();
            level.add(node.val);

            if(flag)
            {
                if(node.left != null)
                    nextLevel.push(node.left);
                if(node.right != null)
                    nextLevel.push(node.right);
            }else
            {
                if(node.right != null)
                    nextLevel.push(node.right);
                if(node.left != null)
                    nextLevel.push(node.left);
            }
        }

        result.add(level);
        temp = curLevel;
        curLevel = nextLevel;
        nextLevel = temp;
        flag = !flag;

    }
    return result;
}
```

