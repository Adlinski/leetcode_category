Strongly Connected Component (SCC)
===

To check if every node has both paths to and from every other node in a given graph:

DFS/BFS from all nodes:
---
[Tarjan's algorithm](https://en.wikipedia.org/wiki/Tarjan%27s_strongly_connected_components_algorithm) supposes every node has a depth `d[i]`. Initially, the root has the smallest depth. And we do the post-order DFS updates `d[i] = min(d[j])` for any neighbor `j` of `i`. Actually BFS also works fine with the reduction rule `d[i] = min(d[j])` here.

    function dfs(i)
        d[i] = i
        mark i as visited
        for each neighbor j of i: 
            if j is not visited then dfs(j)
            d[i] = min(d[i], d[j])

If we call `dfs(root)` in the order of `root = 1,2,..N`, any reachable node `i` from the root would have a depth no less than that root's. In the SCC, a DFS starting from the root will reach itself, causing `d[root] <= d[i] <= d[root]` for any reachable node `i` from `root`. Therefore, all the nodes in SCC will have a depth of `d[root]`. To tell if a graph is a SCC, we check whether all nodes' `d[i]` are the same eventually.

Two DFS/BFS from the single node:
---
It is a simplified version of the [Kosaraju’s algorithm](https://www.geeksforgeeks.org/strongly-connected-components/). Starting from the root, we check if every node can be reached by DFS/BFS. Then, reverse the direction of every edge. We check if every node can be reached from the same root again. See [C++ code](http://codeforces.com/contest/475/submission/8140615).
