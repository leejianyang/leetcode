# 785. Is Graph Bipartite?

完成时间：2019-11-24

原题地址：https://leetcode.com/problems/is-graph-bipartite/

## 题目描述

Given an undirected graph, return true if and only if it is bipartite.

Recall that a graph is bipartite if we can split it's set of nodes into two independent subsets A and B such that every edge in the graph has one node in A and another node in B.

The graph is given in the following form: graph[i] is a list of indexes j for which the edge between nodes i and j exists.  Each node is an integer between 0 and graph.length - 1.  There are no self edges or parallel edges: graph[i] does not contain i, and it doesn't contain any element twice.

Note:

- graph will have length in range [1, 100].
- graph[i] will contain integers in range [0, graph.length - 1].
- graph[i] will not contain i or duplicate values.
- The graph is undirected: if any element j is in graph[i], then i will be in graph[j].

## Example

Example 1:
```
Input: [[1,3], [0,2], [1,3], [0,2]]
Output: true
Explanation: 
The graph looks like this:
0----1
|    |
|    |
3----2
We can divide the vertices into two groups: {0, 2} and {1, 3}.
```

Example 2:
```
Input: [[1,2,3], [0,2], [0,1,3], [0,2]]
Output: false
Explanation: 
The graph looks like this:
0----1
| \  |
|  \ |
3----2
We cannot find a way to divide the set of nodes into two independent subsets.
```

## 我的解法：DFS
```python
import copy

class Solution(object):
    def isBipartite(self, graph):
        """
        :type graph: List[List[int]]
        :rtype: bool
        """
        node_count = len(graph)
        color_map = [0] * node_count
        
        for index in xrange(node_count):
            if color_map[index] != 0:
                continue
            if not self.set_color(graph, color_map, 1, index):
                return False
        return True
        
    def set_color(self, graph, color_map, color, node):
        if color_map[node] <> 0:
            return color_map[node] == color
        color_map[node] = color
        
        for n in graph[node]:
            if not self.set_color(graph, color_map, -color, n):
                return False
        return True
```

## 我的解法：BFS
```python
class Solution(object):
    def isBipartite(self, graph):
        """
        :type graph: List[List[int]]
        :rtype: bool
        """
        node_count = len(graph)
        color_map = [0] * node_count
        
        for index in xrange(node_count):
            if color_map[index] != 0:
                continue
            color_map[index] = 1
            if not self.set_color(graph, color_map, -1, index):
                return False
        
        return True
    
    def set_color(self, graph, color_map, color, node):
        next_round = []
        for n in graph[node]:
            if color_map[n] != 0 and color_map[n] <> color:
                return False
            elif color_map[n] != 0 and color_map[n] == color:
                continue
            else:
                color_map[n] = color
                next_round.append(n)
        
        for n in next_round:
            if not self.set_color(graph, color_map, -color, n):
                return False
        
        return True
```

## 一种更优雅的 BFS 解法

转自[评论区](https://leetcode.com/problems/is-graph-bipartite/discuss/115487/Java-Clean-DFS-solution-with-Explanation)：
```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        int len = graph.length;
        int[] colors = new int[len];
        
        for (int i = 0; i < len; i++) {
            if (colors[i] != 0) continue;
            Queue<Integer> queue = new LinkedList<>();
            queue.offer(i);
            colors[i] = 1;   // Blue: 1; Red: -1.
            
            while (!queue.isEmpty()) {
                int cur = queue.poll();
                for (int next : graph[cur]) {
                    if (colors[next] == 0) {          // If this node hasn't been colored;
                        colors[next] = -colors[cur];  // Color it with a different color;
                        queue.offer(next);
                    } else if (colors[next] != -colors[cur]) {   // If it is colored and its color is different, return false;
                        return false;
                    }
                }
            }
        }
        
        return true;
    }
}
```