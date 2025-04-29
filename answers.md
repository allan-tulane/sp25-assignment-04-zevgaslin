# CMPS 2200 Assignment 5
## Answers

**Name:**Zev Gaslin

- **1a.**
O(d*log_d n).

- **1b.**
- In a d-ary heap, the delete-min operation requires finding the smallest among a node’s d children at each step as we swap downward to restore the heap property, resulting in a total work of O(d*log_d n).

For insert, restoring the heap property only involves swapping the new element upward with its parent at each level, leading to a total work of O(log_d n).
- **1c.**
n = |V| and m = |E|.

Since there are n delete-min operations of work O(d*log_d n). and m insert (or decrease-key) operations of work O(log_d n), the total work is

𝑂(nd*log_d(n)+m*log_d(n)).

- **1d.**
The idea is to choose d to balance the costs of delete-min and insert. For example, if we set d = m/n, the two costs become roughly equal, and the total work is
  O(2m*log₍m/n₎*n),
  which simplifies to
  O(m × (log n) / (log (m/n))).

  Given the assumption that |E| = |V|^(1+ε), we substitute m = n^(1+ε). This gives:

  log n / log (m/n) = log n / log (n^(1+ε)/n) = log n / log (n^ε) = log n / (ε log n) = 1/ε.

  Thus, the overall running time becomes O(m × 1/ε), which simplifies to O(m).
  This matches the desired O(|E|) runtime.


- **2a.**

 k = 0:
0 → 1: weight -2
0 → 2: weight 2
1 → 0: weight -2
1 → 2: weight 0 
2 → 0: weight 2
2 → 1: weight 0

k = 1
0 → 1: weight -2
0 → 2: weight -2
1 → 0: weight -2
1 → 2: weight 0
2 → 0: weight -2
2 → 1: weight 0



k = 2
0 → 1: weight -2
0 → 2: weight -2
1 → 0: weight -2
1 → 2: weight 0
2 → 0: weight -2
2 → 1: weight 0

- **2b.**
APSP(i, j, 2) is the minimum of APSP(i, j, 1) and the path that goes through node 2 once, using APSP(i, 2, 1) + APSP(2, j, 1). You only need APSP(i, j, 1) values to compute APSP(i, j, 2).

our graph is small so all of the paths are already the shortest path by k=1 so nothign changes by k=2, but in a bigger graph k=2 could allow for smaller paths than k=1 does




- **2c.**
APSP(i, j, k) = min(APSP(i, j, k-1), APSP(i, k, k-1) + APSP(k, j, k-1))


- **2d.**
  The work is O(|V|^3) because there are |V|^3 unique combinations of (i, j, k) that need to be considered for APSP(i, j, k)


- **2e.**
Johnson’s algorithm takes O(V × E log E) time, so we prefer the new algorithm when E log E is much smaller than V squared


- **3a.**
Yes, the MST is guaranteed to be a solution to MMET.
By the lightest edge property, if there were another spanning tree with a smaller maximum edge than the MST, we could swap edges and lower the overall weight of the MST, contradicting the fact that it is already minimal. Therefore, the MST minimizes not just the total weight, but also ensures the maximum edge is as small as possible

- **3b.**
Start with the MST. For each edge in the MST, consider removing it and adding a different edge that is not in the MST, making sure the graph stays connected and does not form a cycle. Among all these alternative trees, pick the one with the smallest total weight. This gives the next best spanning tree



- **3c.**
To find the second-best minimum spanning tree, we first find the MST, which takes O(E log E) time. Then, for each of the E edges, we consider replacing one edge in the MST to create an alternative tree. Since this requires checking E swaps, the total work is still O(E^2 + Elog E) or O(E^2)