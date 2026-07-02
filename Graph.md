# Shortest Path with Negative Weights

Difficulty: MEDIUM | Max Score: 50
You are given a directed, weighted graph consisting of V vertices numbered from 0 to V-1 and E directed edges. You are also given a source vertex, src.

Your task is to calculate the minimum distance required to travel from the source vertex to every other vertex in the graph.

Because the graph may contain negative edge weights, you must account for the following special conditions:

Unreachable Nodes: If a vertex is completely unreachable from the source vertex, its shortest distance should be represented as 108 (100000000).
Negative Weight Cycles: If the graph contains a cycle where the sum of the edge weights is strictly less than zero, the shortest paths can decrease infinitely. If such a negative weight cycle exists, shortest paths cannot be reliably computed. In this case, you must simply return -1.

Input Format:

The first line contains three space-separated integers: V (number of vertices), E (number of edges).
The next E lines each contain three space-separated integers u, v, and w, representing a directed edge from vertex u to vertex v with a travel weight of w.
The last line contains a integer src.
Output Format:

If a negative weight cycle exists, print a single integer: -1.
Otherwise, print a single line containing V space-separated integers, where the i-th integer represents the shortest distance from src to vertex i.

Example 1:

Input: 5 5
1 3 2
4 3 -1
2 4 1
1 2 1
0 1 5
0
Output: 0 5 6 6 7
Explanation: Shortest Paths:
For 0 to 1 minimum distance will be 5. By following path 0 → 1
For 0 to 2 minimum distance will be 6. By following path 0 → 1 → 2
For 0 to 3 minimum distance will be 6. By following path 0 → 1 → 2 → 4 → 3
For 0 to 4 minimum distance will be 7. By following path 0 → 1 → 2 → 4

Example 2:

Input: 4 4
0 1 4
1 2 -6
2 3 5
3 1 -2
0
Output: [-1]
Explanation: The graph contains a negative weight cycle formed by the path 1 → 2 → 3 → 1, where the total weight of the cycle is negative.

Constraints:

1 <= V <= 500
1 <= E <= V \* (V - 1)
0 <= src < V
0 <= u, v < V
-105 <= w <= 105

```
/* package package.name; // don't place package name! */
import java.util.*;
import java.lang.*;
import java.io.*;

/* Name of the class has to be "Main" only if the class is public. */
public class Main
{
    static class Pair{
        int u;
        int v;
        int wt;
        Pair(int u,int v,int wt)
        {
            this.u = u;
            this.v = v;
            this.wt = wt;
        }
    }
    public static void main (String[] args) throws java.lang.Exception
    {
        // your code goes here
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int v = Integer.parseInt(st.nextToken());
        int e = Integer.parseInt(st.nextToken());
        List<Pair> edges = new ArrayList<>();
        for(int i=0;i<e;i++)
        {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int V = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            edges.add(new Pair(u,V,w));
        }
        st = new StringTokenizer(br.readLine());
        int src = Integer.parseInt(st.nextToken());
        int[] dist = new int[v];
        int INF = 100000000;
        Arrays.fill(dist,INF);
        dist[src] = 0;;
        for(int i=1;i<=v-1;i++)
        {
            for(Pair p : edges)
            {
                if(dist[p.u]!= INF && dist[p.v]>dist[p.u]+p.wt)
                {
                    dist[p.v]=dist[p.u]+p.wt;
                }
            }
        }
        int cnt = 0;
        for(Pair p : edges)
            {
                if (dist[p.u] != INF &&
                dist[p.v] > dist[p.u] + p.wt) {
                System.out.print(-1);
                return;
            }
            }

        for(int j:dist)
        {
            System.out.print(j+" ");
        }
    }
}
```

---

# Multi-Source Shorted Path

Difficulty: MEDIUM | Max Score: 50
You are given a directed weighted graph with N vertices and M edges. You need to find the shortest distance between every pair of vertices i and j. If no path exists between vertex i and vertex j, the distance should be represented as "INF".

Note: Modify the distances for every pair in place.

Example 1:

Input:
4 4
0 1 5
1 2 3
2 3 1
0 3 10
Output:
0 5 8 9
INF 0 3 4
INF INF 0 1
INF INF INF 0
Explanation: The output represents an N x N matrix where matrix[i][j] is the shortest path from vertex i to vertex j. For instance, the shortest path from vertex 0 to vertex 3 is not the direct edge of weight 10, but rather the path 0 -> 1 -> 2 -> 3 which costs 5 + 3 + 1 = 9.

Example 2:

Input:
3 2
0 1 2
1 0 3
Output:
0 2 INF
3 0 INF
INF INF 0
Explanation: Vertex 2 has no incoming or outgoing edges, so it is disconnected. The distance from any node to vertex 2, and from vertex 2 to any other node, is "INF". The distance from a node to itself is always 0.

Constraints:

1 ≤ N ≤ 100
1 ≤ M ≤ N x (N - 1)
1 ≤ Weight ≤ 1000

```
/* package package.name; // don't place package name! */
import java.util.*;
import java.lang.*;
import java.io.*;

/* Name of the class has to be "Main" only if the class is public. */
public class Main
{
    static class Pair{
        int u;
        int v;
        int w;
        Pair(int u,int v,int w)
        {
            this.u = u;
            this.v = v;
            this.w = w;
        }
    }
    public static void main (String[] args) throws java.lang.Exception
    {
        // your code goes here
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken());
        int[][] dist = new int[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i],Integer.MAX_VALUE);
        }

        for(int i=0;i<n;i++)
        {
            dist[i][i] = 0;
        }
        for(int i=0;i<m;i++)
        {
            st = new StringTokenizer(br.readLine());
            int u = Integer.parseInt(st.nextToken());
            int v = Integer.parseInt(st.nextToken());
            int w = Integer.parseInt(st.nextToken());
            dist[u][v] = w;
        }
        for(int inter = 0;inter<n;inter++)
        {
            for(int src=0;src<n;src++)
            {
                for(int dest=0;dest<n;dest++)
                {
                    if(dist[src][inter]!=Integer.MAX_VALUE &&dist[inter][dest]!=Integer.MAX_VALUE)
                    {
                        dist[src][dest]= Math.min(dist[src][dest],dist[src][inter] + dist[inter][dest]);
                    }
                }
            }
        }
        for(int i=0;i<n;i++)
            {
                for(int j=0;j<n;j++)
                {
                    if(dist[i][j] == Integer.MAX_VALUE)
                        System.out.print("INF ");
                    else
                        System.out.print(dist[i][j] + " ");
                }
                System.out.println();
            }
    }
}
```
