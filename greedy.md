# Minimum Absolute Difference

Given an integer array A of size N, find and return the minimum absolute difference between any two elements in the array.  
We define the absolute difference between two elements ai and aj (where i != j ) as |ai - aj|.

### Input Format

```
The first line of input contains an integer that denotes the number of test cases. Let us denote it by the symbol T.
Each of the test cases contain two lines. The first line of each test case contains an integer, that denotes the value of N. The following line contains N space separated integers, that denote the array elements.
```

### Constraints

```
1 <= T <= 10
2 <= N <= 10^5
0 <= arr[i] <= 10^8
```

### Output Format

```
You have to print minimum difference for each test case in new line.
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
    int n; cin >> n;
    int ans = INT_MAX;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    sort(all(a));
    for (int i = 0; i < n - 1; i++) {
        ans = min(ans, a[i + 1] - a[i]);
    }
    cout << ans << nl;
}

int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    cout << setprecision(15) << fixed;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Activity Selection

You are given n activities with their start and finish times. Select the maximum number of activities that can be performed by a single person, assuming that a person can only work on a single activity at a time.

### Input Format

```
The first line of input contains one integer denoting N.
Next N lines contains two space separated integers denoting the start time and finish time for the ith activity.
```

### Constraints

```
1 ≤ N ≤ 10^6
1 ≤ ai, di ≤ 10^9
```

### Output Format

```
Output one integer, the maximum number of activities that can be performed
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
    int n; cin >> n;
    vector<pii> a(n);
    for (int i = 0; i < n; i++) {
        cin >> a[i].second >> a[i].first;
    }
    sort(all(a));
    int pe = a[0].first, ans = 1;
    for (int i = 1; i < n; i++) {
        if (a[i].second >= pe) {
            ans++;
            pe = a[i].first;
        }
    }
    cout << ans;
}

int32_t main()
{
    fast
    int t = 1;
    //cin >> t;
    precompute();
    cout << setprecision(15) << fixed;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Fractional Knapsack

You are given weights and values of N items. You have to select and put these selected items in a knapsack of capacity W. Select the items in such a way that selected items give the maximum total value possible with given capacity of the knapsack.  
Note: You are allowed to break the items in parts.

### Input Format

```
The first line of input contains two space separated integers, that denote the value of N and W.
Each of the following N lines contains two space separated integers, that denote value and weight, respectively, of the N items.
```

### Constraints

```
1 <= N = 2*10^5
1 <= W <= 10^9
1 <= value, weight <= 10^5
Time Limit: 1 sec
```

### Output Format

```
Print the maximum total value upto six decimal places.
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
#define F first
#define S second
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}

bool comp(pii a, pii b) {
    double v1 = ((double)a.F) / (a.S);
    double v2 = ((double)b.F) / (b.S);
    return v1 > v2;
}
void solve() {
    int n, w; cin >> n >> w;
    vector<pii>a(n);
    for (int i = 0; i < n; i++) cin >> a[i].F >> a[i].S;
    sort(all(a), comp);
    int cw = 0;
    double ans = 0;
    for (int i = 0; i < n; i++) {
        if (a[i].S + cw <= w) {
            ans += a[i].F;
            cw += a[i].S;
        }
        else {
            int d = w - cw;
            ans += d * (((double)a[i].F) / (a[i].S));
            break;
        }
    }
    cout << ans;

}

int32_t main()
{
    fast
    int t = 1;
    //cin >> t;
    precompute();
    cout << setprecision(6) << fixed;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Weighted Job Scheduling

You are given N jobs where every job is represented as:

1. Start Time
2. Finish Time
3. Profit Associated  
   Find the maximum profit subset of jobs such that no two jobs in the subset overlap.

### Input Format

```
The first line of input contains an integer denoting N.
Next N lines contains three space separated integers denoting the start time, finish time and the profit associated with the ith job.
```

### Constraints

```
1 ≤ N ≤ 10^6
1 ≤ ai, di, p ≤ 10^6
```

### Output Format

```
Output one integer, the maximum profit that can be achieved.
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
#define F first
#define S second
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

void precompute() {
}
struct job {
    int start, finish, profit;
};
bool compare(job j1, job j2) {
    return j1.finish < j2.finish;
}
int search(job*a, int n, int idx) {
    int ans = -1;
    int s = 0, e = idx - 1;
    while (s <= e) {
        int mid = s + (e - s) / 2;
        if (a[mid].finish <= a[idx].start) {
            ans = mid;
            s = mid + 1;
        }
        else e = mid - 1;
    }
    return ans;
}
void solve() {
    int n; cin >> n;
    job a[n];
    for (int i = 0; i < n; i++) cin >> a[i].start >> a[i].finish >> a[i].profit;
    sort(a, a + n, compare);
    int dp[n];
    dp[0] = a[0].profit;
    for (int i = 1; i < n; i++) {
        int inc = a[i].profit;
        int idx = search(a, n, i);
        if (idx != -1) inc += dp[idx];

        dp[i] = max(inc, dp[i - 1]);
    }
    cout << dp[n - 1];
}

int32_t main()
{
    fast
    int t = 1;
    //cin >> t;
    precompute();
    cout << setprecision(6) << fixed;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Perimeter with conditions

Aahad gives an array of integers and asks Harshit to find which three elements form a triangle (non-degenerate). The task seems quite easy to Harshit.  
So, Aahad adds some conditions to this task -

1. Find the triangle with maximum perimeter
2. If there are two or more combinations with same value of maximum perimeter, then find the one with the longest side.
3. If there are more than one combinations which satisfy all the above conditions, the find the one with longest minimum side.

### Input Format

```
First line of input contains an integer T, representing the number of test cases.
For each test case, first line contains an integer N, denoting the size of array.
For each test case, the second line contains N space separatated integers, representing the elements of array A[i].
```

### Constraints

```
1 <= T <= 100
1 =< N <= 10^5
1 <= A[i] <= 10^8
Time Limit: 1 second
```

### Output Format

```
The output contains three space-separated elements that denote the length of the sides of triangle. If no such triangle is possible, then print -1.
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
    int n; cin >> n;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    sort(all(a));
    int x = 0, y = 0, z = 0, p = 0;
    for (int i = 0; i < n - 2; i++) {
        int s = a[i] + a[i + 1] + a[i + 2];
        if(a[i]+a[i+1]>a[i+2]){
            if (s >= p) {
            if (s == p) {
                if (a[i + 2] > z) {
                    x = a[i];
                    y = a[i + 1];
                    z = a[i + 2];
                }
                else if (a[i + 2] == z and a[i] > x) {
                    x = a[i];
                    y = a[i + 1];
                    z = a[i + 2];
                }
            }
            else {
                p = s;
                x = a[i];
                y = a[i + 1];
                z = a[i + 2];

            }

        }
        }
    }
    //cout << x << " " << y << " " << z << nl;
    if (x == 0 or y == 0 or z == 0) cout << -1 << nl;
    else cout << x << " " << y << " " << z << nl;
}

int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    cout << setprecision(15) << fixed;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Problem Discussion

Harshit gave Aahad an array of size N. He asked Aahad to minimize the difference between the maximum value and minimum value by modifying the array under some condition. The condition is that each array element either increases or decreases by K (only once).  
The task seems difficult to Aahad, so he has asked you for your help. Are you up to the challenge?

### Input Format

```
First line of input contains an integer T, representing the number of test cases.
For each test case, first line contains two space-separated integers: N, K
Next lines contain N space-separated integers denoting elements of the array
```

### Constraints

```
1 <= T <= 100
1 =< N <= 10^5
1 <= Ai,K <= 10^9
```

### Output Format

```
The output contains a single integer denoting the minimum difference between maximum value and the minimum value in the array
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
    int n, k; cin >> n >> k;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    sort(all(a));
    int mx = a[n - 1] - k;
    int mn = a[0] + k;
    if (mn > mx) swap(mn, mx);
    int ans = a[n - 1] - a[0];
    for (int i = 1; i < n - 1; i++) {
        int s = a[i] - k;
        int b = a[i] + k;
        if (s >= mn or b <= mx) continue;

        if (mx - s <= b - mn) mn = s;
        else mx = b;

    }
    cout << min(ans, mx - mn) << nl;
}

int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    cout << setprecision(15) << fixed;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# King Arthur and Excalibur

King Arthur’s land is in danger. He wants to fend off the Saxon invaders. In order to do so, he needs to find the fabled sword, Excalibur. He has a vague idea about its location, and has dispatched his best Knights and their Squires to acquire it. The Knights go to the location to find The Dark Forest. They set up tents and decided to split into groups to find Excalibur faster. The famous knight, Sir Lancelot was trying to form search parties, but ran into some trouble.  
Most of the knights were untrained for quests, and sending them alone into the dangers of the quest would be a grave mistake. Each of the knights have been given a positive integer parameter by King Arthur, ti - their training score. Sir Lancelot decided that a knight with training t can join the group of t or more knights.  
Some of the knights are very egotistical and can’t work well with others. Hence Sir Lancelot decided it is not necessary to include all the knights, some can stay back and defend the tents from danger. Now Sir Lancelot needs to figure out how many search parties he can organize. Sir Lancelot is one of the most responsible knights and doesn't want to go back to King Arthur empty handed. He would rather die than fail. You need to help him in his quest.

### Input Format

```
First line of input will contain T(number of test cases), each test case follows as.
Line1 : will contain an integer N denoting the total number of explorer
Line2: Will contain N space-separated integers denoting the inexperience level
```

### Constraints

```
1 <= T <= 100
1 <= N <= 10^4
1 <= levels <= N
```

### Output Format

```
For each test case output the answer in a new line.
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
#define F first
#define S second
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
void precompute() {
}

void solve() {
    int n; cin >> n;
    vi a(n + 1);
    for (int i = 1; i <= n; i++) cin >> a[i];
    sort(a.begin() + 1, a.end());
    vi dp(n + 1, 0);
    for (int i = 1; i <= n; i++) {
        if (i - a[i] >= 0) dp[i] = max(dp[i - 1], dp[i - a[i]] + 1);
        else dp[i] = dp[i - 1];
    }
    cout << dp[n] << nl;
}

int32_t main()
{
    fast
    int t = 1;
    cin >> t;
    precompute();
    cout << setprecision(6) << fixed;
    for (int i = 1; i <= t; i++)
        solve();
}
```

# Minimum number of platforms required for a railway

### Code

```

```

# Order

- Minimum Absoute Difference
- Activity Selection
- Fractional Knapsack
- Weighted Job Scheduling
- Perimeter with conditions
- Problem Discussion
- King Arthur and Excalibur
- Minimum number of platforms required for a railway
