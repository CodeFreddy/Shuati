# CourseScheduleII



There are a total of _n_ courses you have to take, labeled from `0` to `n-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

**Example 1:**

```text
Input: 2, [[1,0]] 
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished   
             course 0. So the correct course order is [0,1] .
```

**Example 2:**

```text
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both     
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0. 
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```

**Note:**

1. The input prerequisites is a graph represented by **a list of edges**, not adjacency matrices. Read more about [how a graph is represented](https://www.khanacademy.org/computing/computer-science/algorithms/graph-representation/a/representing-graphs).
2. You may assume that there are no duplicate edges in the input prerequisites.

这道题是course schedule的延伸， 需要将选课顺序排列出来， 同样可以用kahn’s algorithm和dfs做。bfs来做的话也是需要首先简历图之间的关系， 设置每个点的邻居， 然后记录他们的入度。

```java
public class Solution1 {
        /*
         * @param numCourses: a total of n courses
         * @param prerequisites: a list of prerequisite pairs
         * @return: the course order
         */
        public int[] findOrder(int numCourses, int[][] prerequisites) {
            // write your code here
            int[] indegree = new int[numCourses];
            List<List<Integer>> graph = new ArrayList<>(numCourses);
            initialGraph(indegree, graph, prerequisites);
            return BFS(indegree, graph,  numCourses);
        }

        public void initialGraph(int[] indegree, List<List<Integer>> graph, int[][] prerequisites){
            int indLen = indegree.length;
            while(indLen-->0) graph.add(new ArrayList<>());

            for(int[]edge : prerequisites)
            {
                indegree[edge[0]]++;
                graph.get(edge[1]).add(edge[0]);
            }

        }

        public int[] BFS(int[]indegree, List<List<Integer>> graph, int numCourses)
        {
            int[] res = new int[numCourses];
            Queue<Integer> queue = new LinkedList<>();
            for(int i = 0; i < indegree.length; i++)
            {
                if(indegree[i] == 0)
                    queue.offer(i);
            }

            int visited = 0;
            while(!queue.isEmpty())
            {
                int course = queue.poll();
                res[visited++] = course;
                for(Integer aneighbors : graph.get(course))
                {
                    indegree[aneighbors]--;
                    if(indegree[aneighbors] == 0)
                        queue.offer(aneighbors);
                }
            }

            return visited == indegree.length ? res : new int[0];
        }
    }
```



用dfs来做的话初始化也是需要的，然后就是靠递归来执行， 里面有一点，如果该课程的visit是2， 说明该点的子节点全部满足prerequisite并且已经存入结果当中。最后将结果reverse一下就能得到题目想要的答案。

```java
public class Solution2 {
        /*
         * @param numCourses: a total of n courses
         * @param prerequisites: a list of prerequisite pairs
         * @return: the course order
         */
        public int[] findOrder(int numCourses, int[][] prerequisites) {
            // write your code here
            List<Integer> res = new ArrayList<>();
            HashMap<Integer, Integer> visited = new HashMap<>();
            for(int i = 0; i < numCourses; i++)
                visited.put(i, 0);
            List<List<Integer>> graph = new ArrayList<>(numCourses);
            for(int i = 0; i < numCourses; i++)
                graph.add(new ArrayList<>());
            for(int[] edge: prerequisites)
            {
                int ready = edge[0];
                int pre = edge[1];
                graph.get(pre).add(ready);
            }

            for(int i = 0; i < numCourses; i++)
            {
                if(!DFS(res, visited,graph, i)) return new int[0];
            }

            int[]result = new int[numCourses];

            for(int i = 0; i < numCourses; i++)
                result[i] = res.get(numCourses - 1 - i);

            return result;

        }

        public boolean DFS(List<Integer> res, HashMap<Integer, Integer> visited, List<List<Integer>> graph, int course)
        {
            int visit = visited.get(course);

            if(visit == 2)
            {
                return true;
            }else if(visit == 1)
                return false;

            visited.put(course, 1);
            for(Integer aneighbor : graph.get(course))
            {
                if(!DFS(res, visited, graph, aneighbor)) return false;
            }

            visited.put(course, 2);
            res.add(course);
            return true;

        }
    }
```

