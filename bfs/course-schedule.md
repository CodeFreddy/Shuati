# Course Schedule



There are a total of n courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

**Example 1:**

```text
Input: 2, [[1,0]] 
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

**Example 2:**

```text
Input: 2, [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

这其实是一道考察有向无环图（DAG）的题目。也就是需要用到对DAG的拓扑排序 有两种解法 基于BFS的Kahn's algorithm和基于dfs的排序。 这次先使用bfs来解决。知道kahn's 算法后就好做多了 这道题也只是需要返回boolean， 那么设置一个count 变量来记录每一次从queue当中弹出的节点 最后count如果和course的数量相同 说明可以修完所有课（因为这说明这个图是无环图 如果是有环的 count和course number是匹配不上的）。

```java
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int[][]matrix = new int[numCourses][numCourses];
        int[] indegree = new int[numCourses];
        
        for(int i = 0; i < prerequisites.length; i++)
        {
            int ready = prerequisites[i][0];
            int pre = prerequisites[i][1];
            
            if(matrix[pre][ready] == 0)
                indegree[ready]++;
            matrix[pre][ready] = 1;
            
        }
        
    
        int count = 0;
        Queue<Integer>queue = new LinkedList<>();
        for(int i = 0; i < indegree.length; i++)
        {
            if(indegree[i] == 0)
                queue.offer(i);
        }
        
        while(!queue.isEmpty())
        {
            count++;
            int course = queue.poll();
            for(int i = 0; i < numCourses; i++)
            {
                if(matrix[course][i] != 0)
                {
                    indegree[i]--;
                    if(indegree[i] == 0)
                        queue.offer(i);
                }
            }
        }
        
        return count == numCourses;
    }
}
```

