# Standard Result

1. If there is n vertices , then

- Minimum number of edges=0
- Minimum number of edges in connected graph=n-1 that is O(n)
- Number of edges in complete graph=nC2 that is O(n^2)

# DFS on matrix

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
void dfs(vvi &edges, int n, int sv, vi &visited) {
    cout << sv << " ";
    visited[sv] = 1;
    for (int i = 0; i < n; i++) {
        if (i == sv) continue;
        if (edges[sv][i]) {
            if (!visited[i]) dfs(edges, n, i, visited);
        }
    }
}
void solve() {
    int n, e;
    cin >> n >> e;
    vvi edges(n, vi(n, 0));
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        edges[x][y] = 1;
        edges[y][x] = 1;
    }
    vi visited(n, 0);
    dfs(edges, n, 0, visited);
}
int32_t main()
{
    fast
    int t = 1;
    //cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# BFS on Matrix

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
void bfs(vvi &edges, int n, int sv, vi &visited) {
    queue<int>q;
    q.push(sv);
    visited[sv] = true;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";
        for (int i = 0; i < n; i++) {
            if (i == node) continue;
            if (edges[node][i] and !visited[i]) {
                visited[i] = true;
                q.push(i);
            }
        }
    }
}
void solve() {
    int n, e;
    cin >> n >> e;
    vvi edges(n, vi(n, 0));
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        edges[x][y] = 1;
        edges[y][x] = 1;
    }
    vi visited(n, 0);
    for (int i = 0; i < n; i++) {
        if (visited[i] == 0) {
            bfs(edges, n, i, visited);
        }
    }

}
int32_t main()
{
    fast
    int t = 1;
    //cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Has Path

Given an undirected graph G(V, E) and two vertices v1 and v2(as integers), check if there exists any path between them or not. Print true or false.
V is the number of vertices present in graph G and vertices are numbered from 0 to V-1.
E is the number of edges present in graph G.

### Input Format

```
First line will contain T(number of test cases), each test case as follow.
Line 1: Two Integers V and E (separated by space)
Next E lines : Two integers a and b, denoting that there exists an edge between vertex a and vertex b (separated by space)
Line (E+2) : Two integers v1 and v2 (separated by space)
```

### Output Format

```
true or false for each test case in a newline.
```

### Constraints

```
1 <= T <= 10
2 <= V <= 1000
1 <= E <= 1000
0 <= v1, v2 <= V-1
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
bool dfs(vi adj[], int node, vi &visited, int dest) {
    if (node == dest) return true;
    visited[node] = true;
    for (auto nbr : adj[node]) {
        if (!visited[nbr]) {
            bool found = dfs(adj, nbr, visited, dest);
            if (found) return true;
        }
    }
    return false;
}
void solve() {
    int n, e;
    cin >> n >> e;
    vi edges[n];
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        edges[x].push_back(y);
        edges[y].push_back(x);
    }
    vi visited(n, 0);
    int cnt = 0;
    int src, dest; cin >> src >> dest;
    if (dfs(edges, src, visited, dest)) cout << "true\n";
    else cout << "false\n";
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# GET PATH (DFS)

Given an undirected graph G(V, E) and two vertices v1 and v2(as integers), find and print the path from v1 to v2 (if exists). Print nothing if there is no path between v1 and v2.
Find the path using DFS and print the first path that you encountered.
V is the number of vertices present in graph G and vertices are numbered from 0 to V-1.
E is the number of edges present in graph G.
Print the path in reverse order. That is, print v2 first, then intermediate vertices and v1 at last.

### Input

```
First line will contain T(number of test case), each test follow as.
Line 1: Two Integers V and E (separated by space)
Next E lines : Two integers a and b, denoting that there exists an edge between vertex a and vertex b (separated by space)
Line (E+2) : Two integers v1 and v2 (separated by space)
```

### Output

```
Path from v1 to v2 in reverse order (separated by space) for each test case in newline.
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
bool dfs(vi adj[], int node, vi &visited, int dest, vi &path) {
    if (node == dest) {
        path.push_back(node);
        return true;
    }
    visited[node] = true;
    path.push_back(node);
    for (auto nbr : adj[node]) {
        if (!visited[nbr]) {
            bool found = dfs(adj, nbr, visited, dest, path);
            if (found) return true;
        }
    }
    path.pop_back();
    return false;
}
void solve() {
    int n, e;
    cin >> n >> e;
    vi adj[n];
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
    for(int i=0; i<n; i++){
        sort(all(adj[i]));
    }
    vi visited(n, 0);
    int src, dest;
    cin >> src >> dest;
    vi path;
    bool found = dfs(adj, src, visited, dest, path);
    if (found) {
        reverse(all(path));
    }
    for (auto it : path) cout << it << " ";
    cout << endl;


}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# GET PATH (BFS)

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
void bfs(vi adj[], int src, int dest, vi &visited, map<int, int>&parent) {
    queue<int> q;
    q.push(src);
    visited[src] = true;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        for (auto nbr : adj[node]) {
            if (!visited[nbr]) {
                parent[nbr] = node;
                visited[nbr] = true;
                if (nbr == dest) return;
                q.push(nbr);
            }
        }
    }
}
void solve() {
    int n, e;
    cin >> n >> e;
    vi adj[n];
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }
    vi visited(n, 0);
    map<int, int>parent;
    int src, dest;
    cin >> src >> dest;
    bfs(adj, src, dest, visited, parent);
    if (visited[dest]) {
        cout << dest << " ";
        int cur = dest;
        while (parent[cur] != src) {
            cout << parent[cur] << " ";
            cur = parent[cur];
        }
        cout << src;
    }
    cout << endl;

}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Is Connected

Given an undirected graph G(V,E), check if the graph G is connected graph or not.
V is the number of vertices present in graph G and vertices are numbered from 0 to V-1.
E is the number of edges present in graph G.

### Input Format

```
First line will contain T(number of test case), each test case follows as.
Line 1: Two Integers V and E (separated by space)
Next 'E' lines, each have two space-separated integers, 'a' and 'b', denoting that there exists an edge between Vertex 'a' and Vertex 'b'.
```

### Output Format

```
Print "true" or "false" for each test case in new line
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
void bfs(vi edges[], int n, int sv, vi &visited) {
    queue<int>q;
    q.push(sv);
    visited[sv] = true;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        for (auto nbr : edges[node]) {
            if (!visited[nbr]) {
                visited[nbr] = true;
                q.push(nbr);
            }
        }
    }
}
void solve() {
    int n, e;
    cin >> n >> e;
    vi edges[n];
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        edges[x].push_back(y);
        edges[y].push_back(x);
    }
    vi visited(n, 0);
    int cnt=0;
    for (int i = 0; i < n; i++) {
        if (visited[i] == 0) {
            cnt++;
            bfs(edges, n, i, visited);

        }
    }
    if(cnt==1) cout<<"true\n";
    else cout<<"false\n";
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# All Connected Components

Given an undirected graph G(V,E), find and print all the connected components of the given graph G.
V is the number of vertices present in graph G and vertices are numbered from 1 to V.
E is the number of edges present in graph G.
You need to take input in main and create a function which should return all the connected components. And then print them in the main, not inside function.
Print different components in new line. And each component should be printed in increasing order (separated by space). Order of different components doesn't matter.

### Input Format

```
First line of input will contain T(number of test case), each test case follows as.
Line 1: Two Integers V and E (separated by space)
Next 'E' lines, each have two space-separated integers, 'a' and 'b', denoting that there exists an edge between Vertex 'a' and Vertex 'b'.
```

### Output Format

```
For each test case and each connected components print the connected components in sorted order in new line.
Order of connected components doesn't matter (print as you wish).
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
void bfs(vi edges[], int n, int sv, vi &visited, set<int> &path) {
    queue<int>q;
    q.push(sv);
    visited[sv] = true;
    while (!q.empty()) {
        int node = q.front();
        q.pop();
        path.insert(node);
        for (auto nbr : edges[node]) {
            if (!visited[nbr]) {
                visited[nbr] = true;
                q.push(nbr);
            }
        }
    }
}
void solve() {
    int n, e;
    cin >> n >> e;
    vi edges[n + 1];
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        edges[x].push_back(y);
        edges[y].push_back(x);
    }
    vi visited(n+1, 0);
    for (int i = 1; i <= n; i++) {
        set<int> path;
        if (visited[i] == 0) {
            bfs(edges, n, i, visited, path);
            for (auto it : path) cout << it << " ";
            cout << endl;
        }
    }

}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Islands

An island is a small piece of land surrounded by water . A group of islands is said to be connected if we can reach from any given island to any other island in the same group . Given N islands (numbered from 0 to N - 1) and M pair of integers (u and v) denoting island, u is connected to island v and vice versa. Can you count the number of connected groups of islands?

### Input Format

```
The first line of input will contain T(number of test cases), each test case follows as.
Line 1: Two Integers N and M (separated by space)
Next 'M' lines, each have two space-separated integers, 'u' and 'v', denoting that there exists an edge between Vertex 'u' and Vertex 'v'.
```

### Output Format

```
Print number of Islands for each test case in new line.
```

### Constraints

```
1 <= T <= 10
1 <= N <= 1000
1 <= M <= min((N*(N-1))/2, 1000)
0 <= u[i] ,v[i] < N
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}

void dfs(int node, vi adj[], vi &visited) {
    visited[node] = 1;
    //cout << node << " ";
    for (auto nbr : adj[node]) {
        if (!visited[nbr]) dfs(nbr, adj, visited);
    }
}


void solve() {
    int n, e;
    cin >> n >> e;
    vi adj[n];
    for (int i = 0; i < e; i++) {
        int x, y;
        cin >> x >> y;
        adj[x].push_back(y);
        adj[y].push_back(x);
    }

    vi visited(n, 0);
    int cnt = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            cnt++;
            dfs(i, adj, visited);
        }
    }
    cout << cnt << nl;
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Largest Piece

Its Gary's birthday today and he has ordered his favourite square cake consisting of '0's and '1's . But Gary wants the biggest piece of '1's and no '0's . A piece of cake is defined as a part which consist of only '1's, and all '1's share an edge with eachother on the cake. Given the size of cake N and the cake , can you find the size of the biggest piece of '1's for Gary ?

### Input Format

```
First line will contain T(number of test cases), each test case follows as.
Line 1 : An integer N denoting the size of cake
Next N lines : N characters denoting the cake
```

### Output Format

```
Print the size of the biggest piece of '1's and no '0'sfor each test case in a newline.
```

### Constraints

```
1 <= T <= 10
1 <= N <= 1000
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
int dRow[] = { 0, 1, 0, -1 };
int dCol[] = { -1, 0, 1, 0 };
void precompute() {
}
bool isValid(int r, int c, int n) {
    if (r >= 0 and r<n and c >= 0 and c < n) return true;
    return false;
}
int dfs(vector<string>&a, vvi &visited, int r, int c, int n) {
    visited[r][c] = 1;
    int ans = 1;
    for (int i = 0; i < 4; i++) {
        if (isValid(r + dRow[i], c + dCol[i], n) and !visited[r + dRow[i]][c + dCol[i]] and a[r + dRow[i]][c + dCol[i]] == '1') {
            ans += dfs(a, visited, r + dRow[i], c + dCol[i], n);
        }
    }
    return ans;
}
void solve() {
    int n; cin >> n;
    vector<string>a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    vvi visited(n, vi(n, 0));
    int ans = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (a[i][j] == '1' and visited[i][j] == 0) {
                ans = max(ans, dfs(a, visited, i, j, n));
            }
        }
    }
    cout << ans << nl;
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

## Connecting Dots

Gary has a board of size NxM. Each cell in the board is a coloured dot. There exist only 26 colours denoted by uppercase Latin characters (i.e. A,B,...,Z). Now Gary is getting bore and wants to play a game. The key of this game is to find a cycle that contain dots of same colour. Formally, we call a sequence of dots d1, d2, ..., dk a cycle if and only if it meets the following condition:

```
1. These k dots are different: if i ≠ j then di is different from dj.
2. k is at least 4.
3. All dots belong to the same colour.
4. For all 1 ≤ i ≤ k - 1: di and di + 1 are adjacent. Also, dk and d1 should also be adjacent. Cells x and y are called adjacent if they share an edge.
```

Since Gary is colour blind, he wants your help. Your task is to determine if there exists a cycle on the board.

### Input Format

```
Line 1 : Two integers N and M, the number of rows and columns of the board
Next N lines : a string consisting of M characters, expressing colors of dots in each line. Each character is an uppercase Latin letter.
```

### Output Format

```
Return 1 if there is a cycle else return 0
```

### Constraints

```
2 ≤ N, M ≤ 400
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
const int dx4[] = { -1, 0, 1, 0};
const int dy4[] = {0, 1, 0, -1};
void precompute() {
}
bool isValid(int r, int c, int n, int m) {
    return r >= 0 and r<n and c >= 0 and c < m;
}
bool dfs(vector<string>&a, vvi &visited, int r, int c, char ch, int n, int m, int count, int sx, int sy) {

    for (int i = 0; i < n; i++) {
        if (isValid(r + dx4[i], c + dy4[i], n, m) and a[r + dx4[i]][c + dy4[i]] == ch and r + dx4[i] == sx and c + dy4[i] == sy) {
            if (count >= 3) return true;
            return false;
        }
    }
    visited[r][c] = 1;
    for (int i = 0; i < 4; i++) {
        if (isValid(r + dx4[i], c + dy4[i], n, m) and a[r + dx4[i]][c + dy4[i]] == ch and !visited[r + dx4[i]][c + dy4[i]]) {
            bool found = dfs(a, visited, r + dx4[i], c + dy4[i], ch, n, m, count + 1, sx, sy);
            if (found) return true;
        }
    }
    visited[r][c] = 0;
    return false;
}
void solve() {
    int n, m; cin >> n >> m;
    vector<string>a(m);
    for (int i = 0; i < n; i++) cin >> a[i];
    vvi visited(n, vi(m, 0));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (dfs(a, visited, i, j, a[i][j], n, m, 0, i, j)) {
                cout << 1;
                return;
            }
        }
    }
    cout << 0;
}
int32_t main()
{
    fast
    int t = 1;
    //cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# 3 Cycle

Given a graph with N vertices (numbered from 1 to N) and Two Lists (U,V) of size M where (U[i],V[i]) and (V[i],U[i]) are connected by an edge , then count the distinct 3-cycles in the graph. A 3-cycle PQR is a cycle in which (P,Q), (Q,R) and (R,P) are connected an edge.

### Input Format

```
Line 1 : Two integers N and M
Line 2 : List u of size of M
Line 3 : List v of size of M
```

### Output Format

```
The count the number of 3-cycles in the given Graph
```

### Constriants

```
1<=N<=100
1<=M<=(N*(N-1))/2
1<=u[i],v[i]<=N
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}

void solve() {
    int n, m; cin >> n >> m;
    vi u(m), v(m);
    for (int i = 0; i < m; i++) cin >> u[i];
    for (int i = 0; i < m; i++) cin >> v[i];
    vvi a(n + 1, vi(n + 1, 0));
    for (int i = 0; i < m; i++) {
        a[u[i]][v[i]] = 1;
        a[v[i]][u[i]] = 1;
    }
    int ans = 0;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            for (int k = 1; k <= n; k++) {
                if (i == j or j == k or k == i) continue;
                if (a[i][j] == 1 and a[j][k] == 1 and a[k][i] == 1) ans++;
            }
        }
    }
    cout << ans / 6;
}
int32_t main()
{
    fast
    int t = 1;
    //cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# DSU

### Code

```
int findParent(int node, vector<int>&parent) {
    if (node == parent[node]) return node;
    return parent[node] = findParent(parent[node], parent);
}
void Union(int x, int y, vector<int>&parent, vector<int>&rank) {
    x = findParent(x, parent);
    y = findParent(y, parent);
    if (rank[x] > rank[y]) parent[y] = x;
    else if (rank[y] > rank[x]) parent[x] = y;
    else {
        parent[y] = x;
        rank[x]++;
    }
}
```

# Prims Algorithm
Given an undirected, connected and weighted graph G(V, E) with V number of vertices (which are numbered from 0 to V-1) and E number of edges.  
Find and print the total weight of Minimum Spanning Tree (MST) using Prim's algorithm.  
### Input Format
```
First line will contain T(number of test case), each test case follows as. 
Line 1: Two Integers V and E (separated by space)
Next E lines : Three integers ei, ej and wi, denoting that there exists an edge between vertex ei and vertex ej with weight wi (separated by space)
```
### Output Format
```
Weight of MST for each test case in new line.
```
### Constraints
```
1 <= T <= 10
2 <= V, E <= 10^5
1 <= wt <= 10^4
```
### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
const int dx4[] = { -1, 0, 1, 0};
const int dy4[] = {0, 1, 0, -1};
void precompute() {
}

void solve() {
    int n, e; cin >> n >> e;
    vector<pii> adj[n];
    for (int i = 0; i < e; i++) {
        int a, b, w;
        cin >> a >> b >> w;
        adj[a].push_back({b, w});
        adj[b].push_back({a, w});
    }
    vector<int>parent(n, -1);
    vector<int>mst(n, 0);
    vector<int>key(n, INT_MAX);
    int ans = 0;
    key[0] = 0;
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    pq.push({0, 0});
    while (!pq.empty()) {
        pii cur = pq.top();
        pq.pop();
        int node = cur.second;
        if (mst[node]) continue;
        mst[node] = 1;
        ans += key[node];
        for (auto it : adj[node]) {
            int v = it.first;
            int wt = it.second;
            if (mst[v] == 0 and wt < key[v]) {
                key[v] = wt;
                parent[v] = node;
                pq.push({key[v], v});
            }
        }
    }
    cout << ans << nl;
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Kruskals Algorithm
Given an undirected, connected and weighted graph G(V, E) with V number of vertices (which are numbered from 0 to V-1) and E number of edges.  
Find and print the total weight of Minimum Spanning Tree (MST) using Kruskal's algorithm.  
### Input Format
```
First line will contain T(number of test case), each test case follows as. 
Line 1: Two Integers V and E (separated by space)
Next E lines : Three integers ei, ej and wi, denoting that there exists an edge between vertex ei and vertex ej with weight wi (separated by space)
```
### Output Format
```
Weight of MST for each test case in new line.
```
### Constraints
```
1 <= T <= 10
2 <= V, E <= 10^5
1 <= wt <= 10^4
```
### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
const int dx4[] = { -1, 0, 1, 0};
const int dy4[] = {0, 1, 0, -1};
void precompute() {
}
struct edges
{
    int x, y, wt;
};
int findParent(int node, vector<int>&parent) {
    if (node == parent[node]) return node;
    return parent[node] = findParent(parent[node], parent);
}
void Union(int x, int y, vector<int>&parent, vector<int>&rank) {
    x = findParent(x, parent);
    y = findParent(y, parent);
    if (rank[x] > rank[y]) parent[y] = x;
    else if (rank[y] > rank[x]) parent[x] = y;
    else {
        parent[y] = x;
        rank[x]++;
    }
}
bool comp(edges p1, edges p2) {
    return p1.wt < p2.wt;
}
void solve() {
    int n, e; cin >> n >> e;
    vector<edges> adj(e);
    for (int i = 0; i < e; i++) {
        cin >> adj[i].x >> adj[i].y >> adj[i].wt;
    }
    sort(all(adj), comp);
    vector<int>parent(n), rank(n, 0);
    for (int i = 0; i < n; i++) parent[i] = i;
    int cost = 0;
    for(auto &i:adj) {
        if (findParent(i.x,parent) != findParent(i.y,parent)) {
            cost += i.wt;
            Union(i.x, i.y, parent, rank);
        }
    }
    cout << cost << nl;
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Dijkstra Algorithm
Given an undirected, connected and weighted graph G(V, E) with V number of vertices (which are numbered from 0 to V-1) and E number of edges.  
Find and print the shortest distance from the source vertex (i.e. Vertex 0) to all other vertices (including source vertex also) using Dijkstra's Algorithm.  
Print the ith vertex number and the distance from source in one line separated by space. Print different vertices in different lines.  
### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
const int dx4[] = { -1, 0, 1, 0};
const int dy4[] = {0, 1, 0, -1};
void precompute() {
}

void solve() {
    int n, e; cin >> n >> e;
    vector<pii> adj[n];
    for (int i = 0; i < e; i++) {
        int a, b, w;
        cin >> a >> b >> w;
        adj[a].push_back({b, w});
        adj[b].push_back({a, w});
    }
    vector<int>dist(n, INT_MAX);
    priority_queue<pii, vector<pii>, greater<pii>>pq;
    dist[0] = 0;
    pq.push({0, 0});
    while (!pq.empty()) {
        pii cur = pq.top();
        pq.pop();
        int node = cur.second;
        int nodeDistance = cur.first;
        for (auto it : adj[node]) {
            if (nodeDistance + it.second < dist[it.first]) {
                dist[it.first] = nodeDistance + it.second;
                pq.push({dist[it.first], it.first});
            }
        }
    }
    for (int i = 0; i < n; i++) {
        cout << i << " " << dist[i] << nl;
    }
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Bellmanford Algorithm
you are given a weighted directed graph G with n vertices and m edges, and two specified vertex src and des. You want to find the length of shortest paths from vertex src to des. The graph may contain the edges with negative weight.  
### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
const int inf = 1e9;
const int dx4[] = { -1, 0, 1, 0};
const int dy4[] = {0, 1, 0, -1};
void precompute() {
}
struct node {
    int u, v, wt;
};
void solve() {
    int n, m; cin >> n >> m;
    int src, dest; cin >> src >> dest;
    vector<node>edges(m);
    for (int i = 0; i < m; i++) cin >> edges[i].u >> edges[i].v >> edges[i].wt;
    vi dist(n + 1,inf);
    dist[src] = 0;
    for (int i = 1; i <= n - 1; i++) {
        for (auto it : edges) {
            int u = it.u, v = it.v, w = it.wt;
            if (dist[u] != inf and dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
            }
        }
    }
    int f = 0;
    for (auto it : edges) {
        int u = it.u, v = it.v, w = it.wt;
        if (dist[u] != inf and dist[u] + w < dist[v]) {
            f = 1;
            break;
        }
    }
    if (!f) cout << dist[dest] << nl;
    else cout << 1000000000 << nl;

}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Floyd Warshall Algorithm
You are given an undirected weighted graph G with n vertices. And Q queries, each query consists of two integers a and b and you have print the distance of shortest path between a and b.  
Note: If there is no path between a and b print 10^9  
### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

const int dx4[] = { -1, 0, 1, 0};
const int dy4[] = {0, 1, 0, -1};
void precompute() {
}

void solve() {
    int n, m; cin >> n >> m;
    int inf = 1000000000;
    vvi dist(n + 1, vi(n + 1, 0));
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (i == j) dist[i][j] = 0;
            else dist[i][j] = inf;
        }
    }
    for (int i = 0; i < m; i++) {
        int x, y, wt;
        cin >> x >> y >> wt;
        dist[x][y] = min(dist[x][y], wt);
        dist[y][x] = dist[x][y];
        //cout << "#" << dist[x][y] << " " << dist[y][x] << nl;
    }
    for (int k = 1; k <= n; k++) {
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                if (dist[i][k] != inf and dist[k][j] != inf and dist[i][j] > (dist[i][k] + dist[k][j])) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }
    int q; cin >> q;
    while (q--) {
        int x, y;
        cin >> x >> y;
        cout << dist[x][y] << nl;
    }
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Cycle detection in undirected graph using bfs

# Cycle detection in undirected graph using dfs

# Cycle detection in directed graph

# Permutation Swap

Kevin has a permutation P of N integers 1, 2, ..., N, but he doesn't like it. Kevin wants to get a permutation Q.  
He also believes that there are M good pairs of integers (ai, bi). Kevin can perform following operation with his permutation:  
Swap Px and Py only if (x, y) is a good pair.  
Help him and tell if Kevin can obtain permutation Q using such operations.

### Input Format

```
The first line of input will contain an integer T, denoting the number of test cases.

Each test case starts with two space-separated integers N and M. The next line contains N space-separated integers Pi. The next line contains N space-separated integers Qi. Each of the next M lines contains two space-separated integers ai and bi.
```

### Output Format

```
For every test case output "YES" (without quotes) if Kevin can obtain permutation Q and "NO" otherwise.
```

### Constraints

```
1 ≤ T ≤ 10
2 ≤ N ≤ 100000
1 ≤ M ≤ 100000
1 ≤ Pi, Qi ≤ N. Pi and Qi are all distinct.
1 ≤ ai < bi ≤ N
Time Limit: 1 second
```

### Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
const int inf = 2e18;
const int dx4[] = { -1, 0, 1, 0};
const int dy4[] = {0, 1, 0, -1};
void precompute() {
}
struct node {
    int u, v;
};
int findParent(int node, vector<int>&parent) {
    if (node == parent[node]) return node;
    return parent[node] = findParent(parent[node], parent);
}
void Union(int x, int y, vector<int>&rank, vector<int>&parent) {
    x = findParent(x, parent);
    y = findParent(y, parent);
    if (rank[x] > rank[y]) parent[y] = x;
    else if (rank[y] > rank[x]) parent[x] = y;
    else {
        parent[y] = x;
        rank[x]++;
    }
}
void solve() {
    int n, m; cin >> n >> m;
    vector<int>a(n + 1), q(n + 1);
    for (int i = 1; i <= n; i++) cin >> a[i];
    for (int i = 1; i <= n; i++) cin >> q[i];
    vector<node> adj(m);
    for (int i = 0; i < m; i++)
        cin >> adj[i].u >> adj[i].v;

    vector<int>rank(n + 1, 0);
    vector<int>parent(n + 1);
    for (int i = 1; i <= n; i++) {
        parent[i] = i;
    }
    for (int i = 0; i < m; i++) {
        Union(adj[i].u, adj[i].v, rank, parent);
    }
    vector<pii>b(n + 1);
    for (int i = 1; i <= n; i++) {
        b[a[i]].first = i;
        b[q[i]].second = i;

    }
    for (int i = 1; i <= n; i++) {
        if (b[i].first == b[i].second) continue;
        if (findParent(b[i].first, parent) != findParent(b[i].second, parent)) {
            cout << "NO\n";
            return;
        }
    }
    cout << "YES\n";
}
int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    for (int i = 1; i <= t; i++)
        solve();
}

```
