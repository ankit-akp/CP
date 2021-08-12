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
        a[l - 1]++;
        a[r]--;
    }
    for (int i = 1; i <= n; i++) a[i] += a[i - 1];
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
# Substring deletion in binary string
You perform the following operation until the string becomes empty: choose some consecutive substring of equal characters, erase it from the string and glue the remaining two parts together (any of them can be empty) in the same order.

Trick: Here if we h M substrings of equal characters then floor(M/2)+1 is the minimum number of operations for which the entire string can be deleted.
# Maximum Subarray
```
pii maxSubarray(vi &a, int n) {
    int cur = 0, maxi = INT_MIN, e = 0;
    for (int i = 0; i < n; i++) {
        cur += a[i];
        if (cur > maxi) {
            maxi = cur;
            e = i;
        }
        if (cur < 0) cur = 0;
    }
    int s = e;
    while (s >= 0) {
        maxi -= a[s];
        if (maxi == 0) break;
        s--;
    }
    return pii(s, e);
}
```
# Minimum Subarray
```
pii minSubarray(vi &a, int n) {
    vi b(all(a));
    for (int i = 0; i < n; i++) b[i] = b[i] * -1;
    int e, cur = 0, maxi = INT_MIN;
    for (int i = 0; i < n; i++) {
        cur += b[i];
        if (cur > maxi) {
            maxi = cur;
            e = i;
        }
        if (cur < 0) cur = 0;
    }
    int s = e;
    while (s >= 0) {
        maxi -= b[s];
        if (maxi == 0) break;

        s--;
    }
    //cout << s << " " << e << nl;
    return pii(s, e);
}
```
