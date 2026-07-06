https://chiraggupta0.github.io/Super50dsa/Graph

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

# Alien Colony Shield Perimeter

Difficulty: MEDIUM | Max Score: 50
An alien colony is built on a grid-based planetary surface, where:

1 represents an energy shield barrier protecting the colony.
0 represents the hostile outer space surrounding the colony.

The colony's shield is completely surrounded by outer space and consists of one continuous structure (i.e., all shield segments are connected either vertically or horizontally, not diagonally).

There are no enclosed unshielded zones inside the colony (i.e., no trapped spaces).

Each shield segment is a 1x1 energy module, and the goal is to determine the total exposed perimeter of the shield structure, which is the sum of all segments exposed to space.

Note: The region outside the grid is also considered as outer space.

Input Format

The first line contains two integers, R and C — the number of rows and columns in the planetary grid.
The next R lines contain C space-separated integers, where 1 represents a shield module and 0 represents outer space.

Output Format

Print a single integer representing the total exposed perimeter of the colony's shield.

Constraints

1 ≤ R, C ≤ 100
grid[i][j] is 0 or 1.
There is exactly one continuous shield structure in the grid.

Example 1:

Input:
4 4
0 1 0 0
1 1 1 0
0 1 0 0
1 1 0 0

Output:
16

Explanation: The alien shield structure has 16 exposed segments facing open space.

Example 2:

Input:
1 1
1

Output:
4

Explanation: A single 1×1 shield module is fully exposed on all four sides in outer space.

Example 3:

Input:
1 2
1 0

Output:
4
Explanation: The single shield module at (1,1) has four exposed sides, making the total perimeter 4.

### code

```
/* package package.name; // don't place package name! */
import java.util.*;
import java.lang.*;
import java.io.*;

/* Name of the class has to be "Main" only if the class is public. */
public class Main
{
    static class Pair{
        int first;
        int second;
        Pair(int first,int second)
        {
            this.first = first;
            this.second = second;
        }
    }
    public static void main (String[] args) throws java.lang.Exception
    {
        // your code goes here
        int ans = 0;
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        int r = Integer.parseInt(st.nextToken());
        int c = Integer.parseInt(st.nextToken());
        int[][] mat = new int[r][c];

        for(int i=0;i<r;i++)
        {
            st = new StringTokenizer(br.readLine());
            for(int j=0;j<c;j++)
            {
                mat[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        // for(int i=0;i<r;i++)
        // {
        //     for(int j=0;j<c;j++)
        //     {
        //         if(mat[i][j] == 0) continue;
        //         if(i-1<0 ||mat[i-1][j] == 0) ans+=1;
        //         if(i+1>=r ||mat[i+1][j] == 0) ans+=1;
        //         if(j-1<0 ||mat[i][j-1] == 0) ans+=1;
        //         if(j+1>=c ||mat[i][j+1] == 0) ans+=1;
        //     }
        // }
        // System.out.print(ans);
        int[][] vis = new int[r][c];


        Queue<Pair> q = new LinkedList<>();
        for(int i=0;i<r;i++)
        {
            for(int j=0;j<c;j++)
            {
                if(mat[i][j] == 0) continue;
                else
                {
                    q.offer(new Pair(i,j));
                    vis[i][j] = 1;
                    break;
                }
            }
        }
        int[] row = {-1,1,0,0};
        int[] col = {0,0,-1,1};
        while(!q.isEmpty())
        {
            Pair p = q.poll();
            int pr = p.first;
            int pc = p.second;
            for(int j=0;j<4;j++)
            {
                int cl = col[j]+pc;
                int rw = row[j]+pr;
                if(cl<0 || cl>=c || rw<0 || rw>=r)
                {
                    ans+=1;
                    continue;
                }
                if(mat[rw][cl] == 0) ans+=1;
                else if(vis[rw][cl] == 0)
                {
                    vis[rw][cl] = 1;
                    q.offer(new Pair(rw,cl));
                }
            }

        }
        System.out.print(ans);

    }
}
```

# Anoop and Gossip

Difficulty: MEDIUM | Max Score: 50
Anoop lives in a university hostel. Gossip travels fast here. Once someone hears a piece of gossip, they immediately tell it to all their friends, and then those friends tell their friends, and so on. One evening, Anoop comes up with a rumor that he wants to spread across the whole hostel. But nobody is willing to start spreading it for free. Each person demands some number of chocolates before they agree to start gossiping.

The hostel has N students and M pair of friends.
Some pairs of students are friends. If one friend learns the rumor, they will pass it along to their entire circle of friends without asking for more chocolates.
To start the gossip in a circle, Anoop must bribe at least one person from that group.

Find the minimum number of chocolates Anoop needs to spend so that eventually everyone in the hostel knows the rumor.

Input Format

First line of input contains two integers N and M, representing the number of students and number of friendships.
Next line of input contains an array C where Ci represents the number of chocolates that the ith student requires to start a rumor.
Following M lines have a pair of integers (aj, bj) where 0 ≤ aj, bj < N representing a friendship between student aj and student bj.

Output Format

Print a single integer representing the minimum number of chocolates that Anoop needs to spend so that all the N students know about the rumor.

Constraints

1 ≤ N ≤ 105
0 ≤ M ≤ 105
1 ≤ Ci ≤ 109

Example 1:

Input:
6 3
7 2 4 10 6 1
0 1
1 2
4 5

Output:
13

Explanation: Students 0, 1 and 2 form a group and it is optimal to bribe student 1 with 2 chocolates. Student 3 is isolated so we need to give him 10 chocolates. Student 4 and 5 are friends and it is optimal to bribe student 5. Overall, Anoop can spread the rumor in 2 + 10 + 1 = 13 chocolates.

# Center of Graph - 1

Difficulty: EASY | Max Score: 25
"You can always become the star in your own world" ~do4Z

﻿

There is an undirected star graph consisting of N nodes labeled from 1 to N.

A Star Graph is a graph where there is one center node and exactly N - 1 edges that connect the center node with every other node.

You are given N-1 connections listed down and then you have to print the center of that Star Graph.

Input Format:

The first line contains and integer N - representing the number of nodes in the graph.
The next N-1 lines contains two space separated integers representing the N-1 edge connections.

Output Format:

You have to print the node which is center of the start graph.

Example 1:

Input: 5
2 5
3 2
1 2
2 4
Output: 2
Explanation: This graph will be formed like:

                         5
                      1  |  4
                       \ | /
                         2
                         |
                         |
                         3

So, as we can see that center of the graph is 2.

Constraints:

3 <= N <= 1015
