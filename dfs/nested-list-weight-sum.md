# Nested List Weight Sum

#### Description

Given a nested list of integers, return the sum of all integers in the list weighted by their depth. Each element is either an integer, or a list -- whose elements may also be integers or other lists.



#### Example

Given the list `[[1,1],2,[1,1]]`, return `10`. \(four 1's at depth 2, one 2 at depth 1, 4 \* 1 \* 2 + 1 \* 2 \* 1 = 10\)  
Given the list `[1,[4,[6]]]`, return `27`. \(one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4 \* 2 + 6 \* 3 = 27\)

递归解法\(DFS\)：

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        // Write your code here
        if(nestedList == null || nestedList.size() == 0)
        return 0;
        
        return getSum(nestedList, 1);
        
    }
    
    public int getSum(List<NestedInteger> nestedList,  int depth)
    {
        int sum = 0;
        for(NestedInteger i : nestedList)
        {
            if(i.isInteger())
            sum += i.getInteger() * depth;
            else{
             sum += getSum(i.getList(), depth + 1);
            }
        }
        return sum;
    }
}
```

非递归解法\(BFS\)：

```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer,
 *     // rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds,
 *     // if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds,
 *     // if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class Solution {
    public int depthSum(List<NestedInteger> nestedList) {
        // Write your code here
        Queue<NestedInteger> queue = new LinkedList<>();
        for(NestedInteger i: nestedList)
        {
            queue.offer(i);
            
        }
        
        int depth = 0;
        int sum = 0;
        while(!queue.isEmpty())
        {
            int size = queue.size();
            depth++;
            
            for(int i = 0; i < size; i++)
            {
                NestedInteger cur = queue.poll();
                if(cur.isInteger())
                sum += cur.getInteger() * depth;
                else{
                    for(NestedInteger innerList: cur.getList())
                    queue.offer(innerList);
                }
            }
        }
        
        return sum;
        
    }
}
```

