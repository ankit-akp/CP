# Fenwick Tree

## Sum between range L-R

BIT array always has 1 based indexing

### Here given array has 0 based indexing

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
// Sum of given range
// Sum between l-r=query(r)-query(l-1);
//If l==0 ->Sum between l-r=query(r)
void update(int index, int value, vi &BIT, int n) {
    index++;
    for (; index <= n; index += index & (-index)) {
        BIT[index] += value;
    }
}
int query(int index, vi &BIT) {
    int sum = 0;
    index++;
    for (; index > 0; index -= index & (-index)) {
        sum += BIT[index];
    }
    return sum;
}
void solve() {
    int n; cin >> n;
    vi a(n);
    vi BIT(n + 1, 0);
    for (int i = 0; i < n; i++) {
        cin >> a[i];
        update(i, a[i], BIT, n);
    }
    // Here query range in 0 based
    cout << 0 << "->" << 4 << " " << query(4, BIT) << nl;
    cout << 1 << "->" << 4 << " " << query(4, BIT) - query(0, BIT) << nl;
    cout << 1 << "->" << 3 << " " << query(3, BIT) - query(0, BIT) << nl;

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

### Here given array has 1 based indexing

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
// Sum of given range
// Sum between l-r=query(r)-query(l-1);
//If l==0 ->Sum between l-r=query(r)
void update(int index, int value, vi &BIT, int n) {
    for (; index <= n; index += index & (-index)) {
        BIT[index] += value;
    }
}
int query(int index, vi &BIT) {
    int sum = 0;
    for (; index > 0; index -= index & (-index)) {
        sum += BIT[index];
    }
    return sum;
}
void solve() {
    int n; cin >> n;
    vi a(n + 1);
    vi BIT(n + 1, 0);
    for (int i = 1; i <= n; i++) {
        cin >> a[i];
        update(i, a[i], BIT, n);
    }
    cout << 1 << "->" << 5 << " " << query(5, BIT) << nl;
    cout << 2 << "->" << 5 << " " << query(5, BIT) - query(1, BIT) << nl;
    cout << 2 << "->" << 4 << " " << query(4, BIT) - query(1, BIT) << nl;

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
