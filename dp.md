# Note

Step 1: In order to solve DP problem , think for recurrence relation. If you know the recurrence relation for the problem then your problem will be solved easily.
Step 2: Recursion + Memoization
Step 3: Find the relation between problem and subproblem in order to fill dp table.
DP table bharne ke liye pehle ye dekh lo ki dp[n][m](Final answer) kaise fill hoga. Isse idea lg jayega ki table kaise fill hona h. Phir dp[i][j] ke liye aaram se code likh payenge.

# Fibonacci

# Longest Increasing Subsequence

```
#include <bits/stdc++.h>
using namespace std;
#define nl "\n"
#define int long long
int lis(vector<int>&a, int n) {
    vector<int>output(n);
    output[0] = 1;
    for (int i = 1; i < n; i++) {
        int ans = 0;
        for (int j = 0; j < i; j++) {
            if (a[j] <= a[i]) {
                ans = max(ans, output[j]);
            }
        }
        output[i] = ans + 1;
    }
    return *(max_element(output.begin(), output.end()));
}
void solve() {
    int n; cin >> n;
    vector<int>a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    cout << lis(a, n);
}

int32_t main()
{
    int t = 1;
    //cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Stair Case Problem

A child is running up a staircase with n steps and can hop either 1 step, 2 steps or 3 steps at a time. Implement a method to count how many possible ways the child can run up to the stairs. You need to return all possible number of ways.
Time complexity of your code should be O(n).
Since the answer can be pretty large print the answer % mod(10^9 +7)

## Iterative Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007

void solve() {
    int n; cin >> n;
    vector<int>dp(100000 + 1);
    dp[0] = 1;
    dp[1] = 1;
    dp[2] = 2;
    dp[3] = 4;
    for (int i = 4; i <= n; i++) {
        dp[i] = (dp[i - 1] % mod + dp[i - 2] % mod + dp[i - 3] % mod) % mod;
    }
    cout << dp[n] << nl;
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Coin Change Problem

You are given an infinite supply of coins of each of denominations D = {D0, D1, D2, D3, ...... Dn-1}. You need to figure out the total number of ways W, in which you can make a change for Value V using coins of denominations D.
Note : Return 0, if change isn't possible.
W can be pretty large so output the answer % mod(10^9 + 7)

## Input Format

```
First line will contain T (number of test case), each test case is consists of 3 three lines.
Line 1 : Integer n i.e. total number of denominations
Line 2 : N integers i.e. n denomination values
Line 3 : Value V
```

## Recursicve

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
int coinChange(int target, int*a, int n, vector<vector<int>>&dp) {
    //cout << "HERE\n";
    if (target == 0) return 1;
    if (n == 0 or target < 0) return 0;
    if (dp[target][n] != -1) return dp[target][n];
    int first = coinChange(target - a[0], a, n, dp);
    int second = coinChange(target, a + 1, n - 1, dp);
    dp[target][n] = (first%mod + second%mod)%mod;
    return dp[target][n];
}
void solve() {
    int n; cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) cin >> a[i];
    int dom; cin >> dom;

    vector<vector<int>>dp(dom + 1, vector<int>(n + 1, 0));
    for (int i = 0; i <= dom; i++) {
        for (int j = 0; j <= n; j++) dp[i][j] = -1;
    }
    int pos = 0;
    //cout << "HERE1";
    cout << coinChange(dom, a, n, dp) << nl;
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

## Iterative

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007

void solve() {
    int n; cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) cin >> a[i];
    int dom; cin >> dom;

    vector<vector<int>>dp(dom + 1, vector<int>(n, 0));

    for(int i=0; i<n; i++) dp[0][i]=1;
    for(int i=1; i<=dom; i++){
        for(int j=0; j<n; j++){
            if(i-a[j]>=0){
                dp[i][j]+=dp[i-a[j]][j];
            }
            if(j>=1)
            dp[i][j]+=dp[i][j-1];
            dp[i][j]=dp[i][j]%mod;
        }
    }
    cout<<dp[dom][n-1]<<nl;
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Min Cost

Given a cost matrix cost[][] and a position (m, n) in cost[][], write a function that returns cost of minimum cost path to reach (m, n) from (0, 0). Each cell of the matrix represents a cost to traverse through that cell. The total cost of a path to reach (m, n) is the sum of all the costs on that path (including both source and destination). You can only traverse down, right and diagonally lower cells from a given cell, i.e., from a given cell (i, j), cells (i+1, j), (i, j+1), and (i+1, j+1) can be traversed. You may assume that all costs are positive integers

## Recursive Solution

```
int min_cost(vector<vector<int>> &input,int si,int sj,int ei,int ej,vector<vector<int>> &dp){
    if(si==ei and sj==ej) return input[ei][ej];
    if(si>ei or sj>ej) return INT_MAX;
    if(dp[si][sj]!=-1) return dp[si][sj];
    int opt1=min_cost(input,si+1,sj,ei,ej);
    int opt2=min_cost(input,si,sj+1,ei,ej);
    int opt3=min_cost(input,si+1,sj+1,ei,ej);
    //dp[si][sj]=intput[si][sj]+min(opt1,opt2);

    dp[si][sj]=intput[si][sj]+min(opt1,min(opt2,opt3));
    return dp[si][sj];
}
int main(){
    int n,m; cin>>n>>m;
    vector<vector<int>> input(n,vector<int>(m,0));
    vector<vector<int>> dp(n,vector<int>(m,-1));
    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++) cin>>a[i][j];
    }
    cout<<min_cost(input,0,0,n-1,m-1,dp);
}
```

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

## Iterative Solution

```
    int minPathSum(vector<vector<int>>& input) {
        int r=input.size(),c=input[0].size();
        vector<vector<int>> dp(r,vector<int>(c,0));
        dp[r-1][c-1]=input[r-1][c-1];
        for(int i=r-2; i>=0; i--) dp[i][c-1]=dp[i+1][c-1]+input[i][c-1];
        for(int i=c-2; i>=0; i--) dp[r-1][i]=dp[r-1][i+1]+input[r-1][i];
        for(int i=r-2; i>=0; i--){
            for(int j=c-2; j>=0; j--){
                dp[i][j]=input[i][j]+min(dp[i+1][j],dp[i][j+1]);
            }
        }
       return dp[0][0];
    }
```

# Loot Houses(Including Excluding concept)

A thief wants to loot houses. He knows the amount of money in each house. He cannot loot two consecutive houses. Find the maximum amount of money he can loot.

## Input

```
6
5 5 10 100 10 5
```

## Output

```
110
```

## Recursive Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>

int loot(int*a, int n, vi &dp) {
    if (n == 0) return 0;
    if (n == 1) return a[0];
    if (n == 2) return max(a[0], a[1]);
    if (dp[n] != -1) return dp[n];
    int ans1 = a[0] + loot(a + 2, n - 2, dp);
    int ans2 = loot(a + 1, n - 1, dp);
    dp[n] = max(ans1, ans2);
    return dp[n];
}
void solve() {
    int  n; cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) cin >> a[i];
    vi dp(n + 1, -1);
    cout << loot(a, n, dp);
}

int32_t main()
{
    int t = 1;
    //cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

## Iterative Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>

int loot(int*a, int n) {
    if (n == 0) return 0;
    if (n == 1) return a[0];
    if (n == 2) return max(a[0], a[1]);
    vi dp(n + 1, 0);
    dp[0] = a[0];
    dp[1] = max(a[0], a[1]);
    for (int i = 2; i < n; i++) {

        dp[i] = max(dp[i - 1], a[i] + dp[i - 2]);
    }
    return dp[n - 1];
}
void solve() {
    int  n; cin >> n;
    int a[n];
    for (int i = 0; i < n; i++) cin >> a[i];
    cout << loot(a, n);
}

int32_t main()
{
    int t = 1;
    //cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Sam and substring

Samantha and Sam are playing a numbers game. Given a number as a string, no leading zeros, determine the sum of all integer values of substrings of the string.

Given an integer as a string, sum all of its substrings cast as integers. As the number may become large, return the value modulo 1000000007.

```
#define mod 1000000007
int substrings(string str) {
    long cur=str[0]-'0';
    long ans=cur;
    for(int i=1;i<str.size(); i++){
        long c=str[i]-'0';
        cur=((cur*10)%mod+c*(i+1))%mod;
        ans=(ans+cur%mod)%mod;
    }
    return ans;
}

```

# Boredom(Inclusion - Exclusion Concept)

Alex doesn't like boredom. That's why whenever he gets bored, he comes up with games. One long winter evening he came up with a game and decided to play it.

Given a sequence a consisting of n integers. The player can make several steps. In a single step he can choose an element of the sequence (let's denote it ak) and delete it, at that all elements equal to ak + 1 and ak - 1 also must be deleted from the sequence. That step brings ak points to the player.

Alex is a perfectionist, so he decided to get as many points as possible. Help him.

## Constraints

```
1 <= T <= 50
 1 <= N <= 10^5
 1 <= A[i] <= 100000
```

## Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

void solve() {
    int  n; cin >> n;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    vi cnt(100001, 0);
    for (auto i : a) cnt[i]++;
    vi dp(100001, 0);
    dp[0] = 0;
    dp[1] = cnt[1];
    for (int i = 2; i <= 100000; i++) {
        int ans1 = 0, ans2 = 0;
        //Exclusion
        ans1 = dp[i - 1];
        //Inclusion
        if (i - 2 >= 0) ans2 = i * cnt[i] + dp[i - 2];
        dp[i] = max(ans1, ans2);
    }
    cout << *(max_element(all(dp)));
}

int32_t main()
{
    int t = 1;
    //cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Minimum Nuber of Chocolates(Left Dependency and right dependency)

Noor is a teacher. She wants to give some chocolates to the students in her class. All the students sit in a line and each of them has a score according to performance. Noor wants to give at least 1 chocolate to each student. She distributes chocolates to them such that If two students sit next to each other then the one with the higher score must get more chocolates. Noor wants to save money, so she wants to minimise the total number of chocolates.
Note that when two students have equal score they are allowed to have different number of chocolates.

## Input

```
1
4
1 4 4 6
```

## Output

```
6
```

## Note

- ith ki dependecy agr left pe ho aur right pe bhi ho tb ye trick use kr sakte h.
- Ek baar left element ke sath check krke compute kr lenge. Phir ek baar aur iterate krke right element ke sath check kr lenge. Final dp array jo hoga vo humara actual answer hoga.

# Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

void solve() {
    int  n; cin >> n;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    vi dp(n, 0);
    dp[0]=1;

    for (int i = 1; i < n; i++) {
        if(a[i]>a[i-1]) dp[i]=dp[i-1]+1;
        else dp[i]=1;

    }
    for(int i=n-2; i>=0; i--){
        if(a[i]>a[i+1] and dp[i]<=dp[i+1]) dp[i]=dp[i+1]+1;

    }
    int ans = 0;
    for (int i = 0; i < n; i++) ans += dp[i];
    cout << ans << nl;
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Vanya and GCD

Vanya has been studying all day long about sequences and other Complex Mathematical Terms. She thinks she has now become really good at it. So, her friend Vasya decides to test her knowledge and keeps the following challenge it front of her:
Vanya has been given an integer array A of size N. Now, she needs to find the number of increasing sub-sequences of this array with length ≥1 and GCD=1. A sub-sequence of an array is obtained by deleting some (or none) elements and maintaining the relative order of the rest of the elements. As the answer may be large, print it Modulo 109+7
She finds this task really easy, and thinks that you can do it too. Can you?

## Constraints

```
1 <= T <= 50
1 <= N <= 200
1 <= A[i] <= 100
```

## Input

```
1
3
1 2 3
```

## Output

```
5
```

## Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

void solve() {
    int  n; cin >> n;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    vvi dp(n, vi(101, 0));
    // Here dp[i][j] means ith index pe khtm hone wale kitne subsequence ka gcd j h
    dp[0][a[0]] = 1;
    for (int i = 1; i < n; i++) {
        for (int j = i - 1; j >= 0; j--) {
            if (a[i] > a[j]) {
                for (int k = 1; k < 101; k++) {
                    int g = __gcd(k, a[i]);
                    dp[i][g] = (dp[i][g]%mod + dp[j][k]%mod)%mod;
                }
            }
        }
        dp[i][a[i]]++;
    }
    int ans = 0;
    for (int i = 0; i < n; i++) ans = (ans+dp[i][1])%mod;
    cout << ans << nl;

}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Roy and Coin Boxes( Query Trick)

Roy has N coin boxes numbered from 1 to N.
Every day he selects two indices [L,R] and adds 1 coin to each coin box starting from L to R (both inclusive).
He does this for M number of days.
After M days, Roy has a query: How many coin boxes have at least X coins.
He has Q such queries.

## Input

```
First line of will contain T (number of test case), format of each test case follows
First line contains N - number of coin boxes.
Second line contains M - number of days. Each of the next M lines consists of two space separated integers L and R. Followed by integer Q - number of queries.
Each of next Q lines contain a single integer X.a
```

## Output

```
For each query of each test case output the result in a new line.
```

## Sample Input

```
1
7
4
1 3
2 5
1 2
5 6
4
1
7
4
2
```

## Sample Output

```
6
0
0
4
```

## Method 1

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

void solve() {
    int n, m; cin >> n >> m;
    vi dp(n + 1, 0);
    vi s(n + 1, 0);
    vi e(n + 1, 0);
    while (m--) {
        int l, r; cin >> l >> r;
        s[l]++;
        e[r]++;
    }
    dp[1] = s[1];
    //dp[2]=s[1]+s[2]-e[1]
    //dp[3]=s[1]+s[2]+s[3]-e[2]-e[1]
    // dp[i] is how many times 1 is added to ith index
    for (int i = 2; i <= n; i++) {
        dp[i] += dp[i - 1] + s[i] - e[i - 1];
    }

    vi cnt(1000001, 0);
    for (int i = 0; i <= n; i++) {
        cnt[dp[i]]++;
    }
    for (int i =1000000-1; i >= 1; i--) cnt[i] += cnt[i + 1];
    //cnt[0] = n;
    int q; cin >> q;

    while (q--) {
        int x; cin >> x;
        cout << cnt[x] << nl;
    }

}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

## Method 2

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

void solve() {
    int n, m; cin >> n >> m;
    vi a(n + 1, 0);
    while (m--) {
        int l, r; cin >> l >> r;
        a[l]++;
        if (r + 1 <= n)
            a[r + 1]--;
    }
    for (int i = 1; i <= n; i++) a[i] += a[i - 1];
    //for (int i = 0; i <= n; i++) cout << a[i] << " ";
    //cout << nl;
    sort(all(a));
    // for (int i = 0; i <= n; i++) cout << a[i] << " ";
    // return;
    int q; cin >> q;
    while (q--) {
        int x; cin >> x;
        int idx = lower_bound(a.begin() + 1, a.end(), x) - a.begin();
        cout << n - idx + 1 << nl;
    }


}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Alyona and Spreadsheet

During the lesson small girl Alyona works with one famous spreadsheet computer program and learns how to edit tables.
Now she has a table filled with integers. The table consists of n rows and m columns. By ai, j we will denote the integer located at the i-th row and the j-th column. We say that the table is sorted in non-decreasing order in the column j if ai, j ≤ ai + 1, j for all i from 1 to n - 1.
Teacher gave Alyona k tasks. For each of the tasks two integers l and r are given and Alyona has to answer the following question: if one keeps the rows from l to r inclusive and deletes all others, will the table be sorted in non-decreasing order in at least one column? Formally, does there exist such j that ai, j ≤ ai + 1, j for all i from l to r - 1 inclusive.
Alyona is too small to deal with this task and asks you to help!

## Input

```
First line of input will contain T(number of test case), each test case is described as.
The first line of the each test case contains two positive integers n and m the number of rows and the number of columns in the table respectively.
Each of the following n lines contains m integers. The j-th integers in the i of these lines stands for ai, j.

The next line of the input contains an integer k, the number of task that teacher gave to Alyona.

The i-th of the next k lines contains two integers li and ri
```

## Output

```
For each test case, print "Yes" to the i-th line of the output if the table consisting of rows from li to ri inclusive is sorted in non-decreasing order in at least one column. Otherwise, print "No".
```

## Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

void solve() {
    int r, c; cin >> r >> c;
    vvi a(r + 1, vi(c + 1, 0));
    for (int i = 1; i <= r; i++) {
        for (int j = 1; j <= c; j++) cin >> a[i][j];
    }

    vvi dp(r + 1, vi(c + 1, 1));

    for(int i=2; i<=r; i++){
        for(int j=1; j<=c; j++){
            if(a[i][j]>=a[i-1][j]) dp[i][j]=dp[i-1][j];
            else dp[i][j]=i;
        }
    }
    vi mn(r + 1, INT_MAX);
    for (int i = 1; i <= r; i++) {
        for (int j = 1; j <= c; j++) mn[i] = min(mn[i], dp[i][j]);
    }

    int k; cin >> k;
    while (k--) {
        int l, r; cin >> l >> r;
        int d = mn[r];
        if (d <= l) cout << "Yes\n";
        else cout << "No\n";
    }
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}

```

# Longest Common Subsequence

## Recursive Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

int lcs(string str1, string str2, int m, int n, vvi &dp) {
    if (m == 0 or n == 0) return 0;
    if (dp[m][n] != -1) return dp[m][n];
    int ans;
    if (str1[0] == str2[0]) {
        ans = 1 + lcs(str1.substr(1), str2.substr(1), m - 1, n - 1, dp);
    }
    else {
        int opt1 = lcs(str1.substr(1), str2, m - 1, n, dp);
        int opt2 = lcs(str1, str2.substr(1), m, n - 1, dp);
        ans = max(opt1, opt2);
    }
    dp[m][n] = ans;
    return ans;
}
void solve() {
    string str1, str2;
    cin >> str1 >> str2;
    int m = str1.size();
    int n = str2.size();
    vvi dp(m + 1, vi(n + 1, -1));
    cout << lcs(str1, str2, m, n, dp)<<nl;;
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

## Iterative Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()


void solve() {
    string str1, str2;
    cin >> str1 >> str2;
    int m = str1.size();
    int n = str2.size();
    vvi dp(m + 1, vi(n + 1, 0));
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (str1[i - 1] == str2[j - 1]) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            }
            else dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
        }
    }
    cout << dp[m][n] << nl;

}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Knapsnack - Problem (Inclusion - Exclusion Concept)

A thief robbing a store and can carry a maximal weight of W into his knapsack. There are N items and ith item weigh wi and is of value vi. What is the maximum value V, that thief can take ?
Note: Space complexity should be O(W).

## Input

```
Line 1 : N i.e. number of items
Line 2 : N Integers i.e. weights of items separated by space
Line 3 : N Integers i.e. values of items separated by space
Line 4 : Integer W i.e. maximum weight thief can carry
```

## Output

```
Line 1 : Maximum value V
```

Recurrence Relation: K(i,W)=max(val[i-1]+K(i-1,W-wt[i-1]),K(i-1,W))
We will include val[i-1] only if W-wt[i-1]>=0.

## Recursive Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

int knapsack(int n, vi &wt, vi &val, int w, int pos, vvi &dp) {
    //Base Case
    if (pos == n or w == 0) return 0;
    //Recursive Case
    if (dp[w][pos] != -1) return dp[w][pos];
    int ans1 = 0, ans2 = 0;
    if (w - wt[pos] >= 0) {
        ans1 = val[pos] + knapsack(n, wt, val, w - wt[pos], pos + 1, dp);
    }
    ans2 = knapsack(n, wt, val, w, pos + 1, dp);
    return dp[w][pos] = max(ans1, ans2);
}
void solve() {
    int n; cin >> n;
    vi wt(n), v(n);
    for (int i = 0; i < n; i++) cin >> wt[i];
    for (int i = 0; i < n; i++) cin >> v[i];
    int w; cin >> w;
    vvi dp(w + 1, vi(n, -1));
    cout << knapsack(n, wt, v, w, 0, dp);
}

int32_t main()
{
    int t = 1;
    //cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

## Iterative Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

int knapsack(int n, vi &wt, vi &val, int w) {
    vvi dp(n + 1, vi(w + 1));
    for (int i = 0; i <= w; i++) dp[0][i] = 0;
    for (int i = 0; i <= n; i++) dp[i][0] = 0;

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= w; j++) {
            dp[i][j] = dp[i - 1][j];
            if (j - wt[i - 1] >= 0) dp[i][j] = max(dp[i][j], val[i - 1] + dp[i - 1][j - wt[i - 1]]);
        }
    }
    return dp[n][w];
}
void solve() {
    int n; cin >> n;
    vi wt(n), v(n);
    for (int i = 0; i < n; i++) cin >> wt[i];
    for (int i = 0; i < n; i++) cin >> v[i];
    int w; cin >> w;
    vvi dp(w + 1, vi(n, -1));
    cout << knapsack(n, wt, v, w);
}

int32_t main()
{
    int t = 1;
    //cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Subset Sum

Given an array of n integers, find if a subset of sum k can be formed from the given set. Print Yes or No.

## Input

```
First-line will contain T(number of test cases), each test case consists of three lines.
First-line contains a single integer N(length of input array).
Second-line contains n space-separated integers denoting the elements of array.
The last line contains a single positive integer k.
```

## Output

```
Output Yes if there exists a subset whose sum is k, else output No for each test case in new line.
```

## Recursive Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

int helper(vi &val, int n, int sum, vvi &dp) {
    // Base Case
    if (sum == 0) return 1;
    if(sum<0) return 0;
    if (n <= 0) return 0;
    // Recursive case
    if (dp[n][sum] != -1) return dp[n][sum];
    bool opt1 = helper(val, n - 1, sum - val[n - 1], dp);
    bool opt2 = helper(val, n - 1, sum, dp);
    return dp[n][sum] = (opt1 or opt2);
}
void solve() {
    int n; cin >> n;
    vi val(n);
    for (int i = 0; i < n; i++) cin >> val[i];

    int sum; cin >> sum;
    vvi dp(n + 1, vi(sum + 1, -1));
    if (helper(val, n, sum, dp)) cout << "Yes\n";
    else cout << "No\n";
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

## Iterative Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

int helper(vi &val, int n, int sum) {
    vvi dp(n + 1, vi(sum + 1, 0));
    for (int i = 0; i <= n; i++) dp[i][0] = 1;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            dp[i][j] = dp[i - 1][j];
            if (j - val[i - 1] >= 0) dp[i][j] = dp[i][j] or dp[i - 1][j - val[i - 1]];
        }
    }
    return dp[n][sum];
}
void solve() {
    int n; cin >> n;
    vi val(n);
    for (int i = 0; i < n; i++) cin >> val[i];

    int sum; cin >> sum;
    if (helper(val, n, sum)) cout << "Yes\n";
    else cout << "No\n";
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

## Iterative + Space Optimization Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

int helper(vi &val, int n, int sum) {
    vvi dp(2, vi(sum + 1, 0));
    for (int i = 0; i <= 1; i++) dp[i][0] = 1;
    int flag = 1;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {
            dp[flag][j] = dp[flag ^ 1][j];
            if (j - val[i - 1] >= 0) dp[flag][j] = dp[flag][j] or dp[flag ^ 1][j - val[i - 1]];
        }
        flag=flag ^ 1;
    }
    return dp[flag ^ 1][sum];
}
void solve() {
    int n; cin >> n;
    vi val(n);
    for (int i = 0; i < n; i++) cin >> val[i];

    int sum; cin >> sum;
    if (helper(val, n, sum)) cout << "Yes\n";
    else cout << "No\n";
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Mehta and Bank Robbery - Problem(3D DP Similar to Knapsack)

One fine day, when everything was going good, Mehta was fired from his job and had to leave all the work. So, he decided to become a member of gangster squad and start his new career of robbing. Being a novice, mehta was asked to perform a robbery task in which he was given a bag having a capacity W units. So, when he reached the house to be robbed, there lay N items each having particular weight and particular profit associated with it. But, theres a twist associated, He has first 10 primes with him, which he can use atmost once, if he picks any item x, then he can multiply his profit[x] with any of the first 10 primes and then put that item into his bag. Each prime can only be used with one particular item and one item can only have atmost one prime multiplied with its profit. Its not necessary to pick all the items. If he doesnt want to use a prime with any particular item, he can simply add the profit as it is, more specifically, 1\*profit[x] for xth item will get added to its total profit, and that he can do with as many items as he wants. He cannot fill his bag more than weight W units. Each item should be picked with its whole weight, i.e it cannot be broken into several other items of lesser weight. So, now to impress his squad, he wishes to maximize the total profit he can achieve by robbing this wealthy house.

## Input

```
The first line of input will contain T(number of test cases), each test will follow as.
First Line will contain two integers N and W (number of items and maximum weight respectively).
Second-line will contain N space-separated integers denoting the profit associated with the Ith item.
The third line will contain N space-separated integers denoting the weight of the Ith item.
```

## Output

```
Output the maximum profit obtainable for each test case in a new line.
```

## Sample Input

```
1
7 37
33 5 14 14 16 25 15
5 19 30 4 15 31 25
```

## Sample Output

```
1591
```

## Code

```
#include <bits/stdc++.h>
using namespace std;
#define int long long
#define nl "\n"
#define mod 1000000007
#define vvi vector<vector<int>>
#define vi vector<int>
#define all(v) v.begin(), v.end()

void solve() {
    int n, w; cin >> n >> w;
    vector<pair<int, int>>a(n);
    for (int i = 0; i < n; i++) cin >> a[i].first;
    for (int i = 0; i < n; i++) cin >> a[i].second;
    sort(all(a));
    int dp[2][n + 1][w + 1];
    for (int i = 0; i < 2; i++) {
        for (int j = 0; j <= n; j++) {
            for (int k = 0; k <= w; k++) dp[i][j][k] = 0;
        }
    }
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= w; j++) {
            dp[0][i][j] = dp[0][i - 1][j];
            if (j >= a[i - 1].second) dp[0][i][j] = max(dp[0][i][j], dp[0][i - 1][j - a[i - 1].second] + a[i - 1].first);
        }
    }
    int primes[11] = {1, 2, 3, 5, 7, 11, 13, 17, 19, 23, 29};
    for (int prime = 1; prime <= 10; prime++) {
        int p = prime % 2;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= w; j++) {
                dp[p][i][j] = dp[p][i - 1][j];
                if (j >= a[i].second) {
                    dp[p][i][j] = max(dp[p][i][j], dp[p][i - 1][j - a[i].second] + a[i].first);
                    dp[p][i][j] = max(dp[p][i][j], dp[p ^ 1][i - 1][j - a[i].second] + a[i].first * primes[prime]);
                }
            }
        }
    }
    cout << dp[0][n][w] << nl;
}

int32_t main()
{
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Maximum Sum Rectangle

Given a 2D array, find the maximum sum rectangle in it. In other words find maximum sum over all rectangles in the matrix.

## Input

```
First line of input will contain T(number of test case), each test case follows as.
First line contains 2 numbers n and m denoting number of rows and number of columns. Next n lines contain m space separated integers denoting elements of matrix nxm.
```

## Output

```
Output a single integer, maximum sum rectangle for each test case in a newline.
```

## Code

```
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define nl "\n"
    #define mod 1000000007
    #define vvi vector<vector<int>>
    #define vi vector<int>
    #define all(v) v.begin(), v.end()
    int kadane(vi &a, int n) {
        int cur = 0, maxi = INT_MIN, s = 0, sa = 0, ea = 0;
        for (int i = 0; i < n; i++) {
            cur += a[i];
            if (cur > maxi) maxi = cur;

            if (cur < 0) cur = 0;
        }
        return maxi;
    }
    void solve() {
        int r, c; cin >> r >> c;
        vvi a(r, vi(c, 0));
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) cin >> a[i][j];
        }

        int left = 0, right = 0, ans = INT_MIN;
        while (left < c) {
            right = left;
            vi cnt(r, 0);
            while (right < c) {
                for (int i = 0; i < r; i++) {
                    cnt[i] += a[i][right];
                }
                right++;
                ans = max(ans, kadane(cnt, r));
            }
            left++;
        }
        cout << ans << nl;
    }

    int32_t main()
    {
        int t = 1;
        cin >> t;
        for (int i = 1; i <= t; i++)
            solve();
    }
```

# Smallest Super-sequence

Given two strings S and T, find and return the length of their smallest super-sequence.
A shortest super sequence of two strings is defined as the shortest possible string containing both strings as subsequences.
Note that if the two strings do not have any common characters, then return the sum of lengths of the two strings.

## Approach

- Find Longest Common Subsequence (lcs) of two given strings.
- Insert non-lcs characters (in their original order in strings) to the lcs found above, and return the result.

## Code

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

int LCS(string str1, string str2) {
    int l1 = str1.size(), l2 = str2.size();
    vvi dp(l1 + 1, vi(l2 + 1, 0));
    for (int i = 1; i <= l1; i++) {
        for (int j = 1; j <= l2; j++) {
            if (str1[i - 1] == str2[j - 1]) dp[i][j] = 1 + dp[i - 1][j - 1];
            else {
                dp[i][j] = dp[i - 1][j];
                dp[i][j] = max(dp[i][j], dp[i][j - 1]);
            }
        }
    }
    return dp[l1][l2];
}
void solve() {
    string str1; cin >> str1;
    string str2; cin >> str2;
    int l1 = str1.size(), l2 = str2.size();
    cout << l1 + l2 - LCS(str1, str2) << nl;
}

int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Job Assignment Problem(DP with Bitmasking)

Let there be N workers and N jobs. Any worker can be assigned to perform any job, incurring some cost that may vary depending on the work-job assignment. It is required to perform all jobs by assigning exactly one worker to each job and exactly one job to each agent in such a way that the total cost of the assignment is minimized.

## Recursice Code

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

int minCost(int cost[4][4], int n, int p, int mask, vi &dp) {
    if (p >= n) return 0;
    if (dp[mask] != INT_MAX) return dp[mask];
    int mn = INT_MAX;
    for (int i = 0; i < n; i++) {
        if (!(mask & (1 << i))) {
            int ans = minCost(cost, n, p + 1, mask | (1 << i), dp) + cost[p][i];
            mn = min(mn, ans);
        }
    }
    return dp[mask] = mn;
}
void solve() {
    int n = 4;
    int cost[4][4] = {{10, 2, 6, 5}, {1, 15, 12, 8}, {7, 8, 9, 3}, {15, 13, 4, 10}};
    vi dp((1 << n), INT_MAX);

    cout << minCost(cost, 4, 0, 0, dp) << nl;
}

int32_t main()
{
    fast
    int t = 1;
    //cin >> t;

    for (int i = 1; i <= t; i++)
        solve();
}
```

## Iterative Code

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

int minCost(int cost[4][4], int n) {
    int* dp = new int[(1 << n)];
    for (int i = 0; i < (1 << n); i++) dp[i] = INT_MAX;
    dp[0] = 0;
    for (int mask = 0; mask < ((1 << n) - 1); mask++) {
        int k = __builtin_popcount(mask);
        for (int j = 0; j < n; j++) {
            if (!(mask & (1 << j))) {
                dp[mask | (1 << j)] = min(dp[mask | (1 << j)], dp[mask] + cost[k][j]);
            }
        }
    }
    return dp[(1 << n) - 1];
}
void solve() {
    int cost[4][4] = {{10, 2, 6, 5}, {1, 15, 12, 8}, {7, 8, 9, 3}, {15, 13, 4, 10}};
    cout << minCost(cost, 4) << nl;
}

int32_t main()
{
    fast
    int t = 1;
    //cin >> t;

    for (int i = 1; i <= t; i++)
        solve();
}
```
