# Graph Valid Tree

#### Description

Given `n` nodes labeled from `0` to `n - 1` and a list of `undirected` edges \(each edge is a pair of nodes\), write a function to check whether these edges make up a valid tree.

You can assume that no duplicate edges will appear in edges. Since all edges are `undirected`, `[0, 1]` is the same as `[1, 0]` and thus will not appear together in edges.Have you met this question in a real interview?  Yes

#### Example

Given `n = 5` and `edges = [[0, 1], [0, 2], [0, 3], [1, 4]]`, return true.

Given `n = 5` and `edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]`, return false.

这道题是给一个无向图来判断是否能组成一个valid tree。如果是一颗树意味着所有的node都是连通的，并且是无环的。用bfs来做的话就需要一个queue来访问每一个点和他的邻居，然后拿一个hashset来放节点作为结果，如果hashset里的node数量等于n，说明没有环，返回true，否则返回false。当然一开始需要建立一下图中各个点的关系。

```java
public class Solution {
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        // write your code here
        if(edges.length != n - 1)
        return false;
        if(n == 0)
        return false;
        
        Set<Integer> hash = new HashSet<>();
        List<List<Integer>> graph = new ArrayList<>(n);
        for(int i = 0; i < n; i++)
            graph.add(new ArrayList<>());
            
        for(int i = 0; i < n - 1; i++)
        {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(0);
        hash.add(0);
        
        while(!queue.isEmpty())
        {
            int current = queue.poll();
            for(Integer aneighbors: graph.get(current))
            {
                if(hash.contains(aneighbors))
                continue;
                
                hash.add(aneighbors);
                queue.offer(aneighbors);
            }
        }
        
        return hash.size() == n;
    }
}
```

用dfs来做， 首先也是先需要建立一个图的链接， 然后需要一个boolean类型的数租visited来存放每个点是否被访问过， 任意选一个点， 进入dfs， 如果此时该点已经被访问过， 说明有环，return false， 否则将该点的visited设置为true，然后继续遍历它的邻居节点。 这里需要记录上一个节点的信息， 这样避免回到上一个节点。最后执行完dfs，再遍历一遍visited数组，看是不是每个点都被访问过了 如果有false的节点，说明不是连通的， 那么也return false；

```java
public class Solution {
    /**
     * @param n: An integer
     * @param edges: a list of undirected edges
     * @return: true if it's a valid tree, or false
     */
    public boolean validTree(int n, int[][] edges) {
        // write your code here
        if(n == 0) return false;
        if(n - 1!= edges.length) return false;
        
        List<List<Integer>> graph = new ArrayList<>();
        for(int i = 0; i < n; i++)
        {
            graph.add(new ArrayList<>());
        }
        for(int i = 0; i < edges.length; i++)
        {
            int u = edges[i][0];
            int v = edges[i][1];
            graph.get(u).add(v);
            graph.get(v).add(u);
        }
        
        boolean[] visited = new boolean[n];
        for(int i = 0; i < n; i++)
        {
            visited[i] = false;
        }
        
        if(!DFS(graph, 0, -1, visited)) return false;
        
        for(boolean i: visited)
        {
            if(!i) return false;
        }
        
        return true;
        
    }
    
    public boolean DFS(List<List<Integer>>graph, int cur, int pre, boolean[] visited)
    {
    
        if(visited[cur] == true)
        return false;
        
        visited[cur] = true;
        
        for(Integer aneighbors: graph.get(cur))
        {
            if(aneighbors != pre)
        {
            if(!DFS(graph, aneighbors, cur, visited)) return false;
        }
            
            
        }
        return true;
    }
}
```

