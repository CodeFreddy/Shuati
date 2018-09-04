# Connected Component in Undirected Graph

#### Description

Find the number connected component in the undirected graph. Each node in the graph contains a label and a list of its neighbors. \(a connected component \(or just component\) of an undirected graph is a subgraph in which any two vertices are connected to each other by paths, and which is connected to no additional vertices in the supergraph.\)

Each connected component should sort by label.Have you met this question in a real interview?  Yes

#### Clarification

[Learn more about representation of graphs](http://www.lintcode.com/help/graph)

#### Example

Given graph:

```text
A------B  C
 \     |  | 
  \    |  |
   \   |  |
    \  |  |
      D   E
```

Return `{A,B,D}, {C,E}`. Since there are two connected component which is `{A,B,D}, {C,E}`

`这道题和clone graph一样都是跟无向图打交道， 题意要我们根据输入的一堆node返回能够构成图的节点组成的list。`

`为了避免重复访问 所以用到了hashmap， 设置一个visited的hashmap去检查一个节点是否被访问过， 如果没有 就进行处理。最后返回结果。`

```java
public class Solution {
    /*
     * @param nodes: a array of Undirected graph node
     * @return: a connected set of a Undirected graph
     */
    public List<List<Integer>> connectedSet(List<UndirectedGraphNode> nodes) {
        // write your code here
        List<List<Integer>> result = new ArrayList<>();
        if(nodes == null) return  result;

        HashMap<UndirectedGraphNode, Boolean> visited = new HashMap<>();
        for(UndirectedGraphNode node: nodes)
        {
            visited.put(node, false);

        }

        for(UndirectedGraphNode node: nodes)
        {
            if(visited.get(node) == false)
            {
                bfs(node, visited, result);
            }
        }

        return result;
    }

    public void bfs(UndirectedGraphNode node, HashMap<UndirectedGraphNode, Boolean> visited, List<List<Integer>> result)
    {
        List<Integer> level = new ArrayList<>();
        Queue<UndirectedGraphNode> queue = new LinkedList<>();
        queue.offer(node);
        visited.put(node, true);

        while(!queue.isEmpty())
        {
            UndirectedGraphNode curNode = queue.poll();
            level.add(curNode.label);
            for(UndirectedGraphNode aneighbor: curNode.neighbors)
            {
                if(visited.get(aneighbor) == false)
                {
                    visited.put(aneighbor,true);
                    queue.offer(aneighbor);
                }
            }
        }
        Collections.sort(level);
        result.add(level);
    }
}
```

 ``

