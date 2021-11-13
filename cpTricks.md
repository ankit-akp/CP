# TEMPLATE

```
#include <bits/stdc++.h>
using namespace std;

#define int long long
#define ull unsigned long long
#define ld long double
#define eb emplace_back
#define pb push_back
#define pf push_front
#define F first
#define S second
#define mp make_pair
#define vi vector<int>
#define vvi vector<vector<int>>
#define vs vector<string>
#define vpii vector<pii>
#define all(v) v.begin(), v.end()
#define allcomp(v) v.begin(), v.end(), comp
#define pii pair<int, int>
#define sz(v) ((int)(v).size())
#define init(arr, val) memset(arr, val, sizeof(arr))
#define rep(i, a, b) for (int i = a; i < b; i++)
#define pp(n) printf("%.10Lf", n);
#define nl "\n"
#define ppc        __builtin_popcount
#define ppcll      __builtin_popcountll
const int special_prime = 982451653l; // The 50,000,000th prime number
const int mod = 1e9 + 7; // Prime Number
const int inf = 2e18;
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);
/// Tip : If a and b are positive integers ; we may say - ceil (a/b) = 1 + floor ( (a-1)/b )=(a+b-1)/b

//VECTOR
template <class T>
istream &operator>>(istream &in, vector<T> &a)
{
    for (auto &i : a)
        cin >> i;
    return in;
}
template <class T>
ostream &operator<<(ostream &out, const vector<T> &a)
{
    for (auto &i : a)
        cout << i << " ";
    return out;
}

// Mathematical Function
int power(int x, int y, int p = mod)
{
    unsigned long long res = 1; // Initialize result

    x = x % p;
    while (y > 0)
    {
        if (y & 1)
            res = (res * x) % p;

        y = y >> 1;
        x = (x * x) % p;
    }
    return res;
}

// Returns n^(-1) mod p
int modInverse(int n, int p = mod)
{
    return power(n, p - 2, p);
}

void precompute() {
}


void solve(int T)
{

}

int32_t main()
{
    // freopen("input.txt", "r", stdin);
    // freopen("output.txt", "w", stdout);
    fast
    int t = 1;
    cin >> t;
    //cin >> ws;
    precompute();
    cout << setprecision(8) << fixed;

    for (int i = 1; i <= t; i++)
        solve(i);
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

# https://www.codechef.com/problems/COWA19B

Given a number N, which is the size of array where indices are from 1 to N . Initially all the elements of array are 0 . Q queries are given . Each query contains two variables L and R . For each query you have to perform the following operation : for each index i where L<=i<=R you have to add a value of of (i-L+1) to the array element at index i . After performing Q queries, a number M is given. It is followed by M number of indices (I) where, for each index you have to output the value of element present in that index (I) of array.

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
inline size_t key(int i, int j) {return (size_t) i << 32 | (unsigned int) j;}

void precompute() {
}
struct node
{
    int live, damage, index;
};
bool comp(node p1, node p2) {
    p1.damage > p2.damage;
}
void solve() {
    int n; cin >> n;
    vi a(n + 1, 0);
    vi cnt(n + 2, 0);
    vi ans(n + 2, 0);
    int q; cin >> q;
    while (q--) {
        int l, r; cin >> l >> r;
        cnt[l]++;
        cnt[r + 1]--;
        ans[r + 1] -= r - l + 1;
    }
    for (int i = 1; i <= n; i++) cnt[i] += cnt[i - 1];
    for (int i = 1; i <= n; i++) ans[i] += ans[i - 1] + cnt[i];
    int m; cin >> m;
    while (m--) {
        int x;
        cin >> x;
        cout << ans[x] << nl;
    }


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

# Same Interger

You are given three integers A, B and C. Find the minimum number of operations required to make A, B and C all equal by repeatedly performing the following two kinds of operations in any order:

Choose two among A, B and C, then increase both by 1.  
Choose one among A, B and C, then increase it by 2.  
It can be proved that we can always make A, B and C all equal by repeatedly performing these operations.

### Code

```
void solve(int T)
    {
        int a, b, c; cin >> a >> b >> c;
        int s = a + b + c;
        int x = max(a, max(b, c));
        int ans = 0;
        while (true) {
            if ((3 * x - s) & 1) x++;
            else {
                if (3 * x % 2 == s % 2) {
                    ans = (3 * x - s) / 2;
                    break;
                }
                else x++;
            }
        }
        cout << ans;
    }
```

### Editorial

```
Suppose that when you finish the operations, all integers are X. Since the sum of three integers always
increases by two in each operation, the total number of operations is (3X − (A + B + C))/2. Thus, we
want to minimize X.
Let M be the maximum of A, B, C. Since we can never decrease integers, X ≥ M must hold. Also,
since we can never change the parity of sum of three integers, 3X ≡ A+B +C (mod 2) must hold. (It’s
easy to see that these are sufficient conditions).
Therefore,
• If 3M ≡ A + B + C (mod 2), X = M.
• Otherwise, X = M + 1.
and we should print (3X − (A + B + C))/2.
```

# Special Numbers

Theofanis really likes sequences of positive integers, thus his teacher (Yeltsa Kcir) gave him a problem about a sequence that consists of only special numbers.

Let's call a positive number special if it can be written as a sum of different non-negative powers of n. For example, for n=4 number 17 is special, because it can be written as 40+42=1+16=17, but 9 is not.

Theofanis asks you to help him find the k-th special number if they are sorted in increasing order. Since this number may be too large, output it modulo 109+7.

### Code

```
int fastPower(int a, int b, int m = mod) {
    int res = 1;
    while (b) {
        if (b & 1) res = (res % m * a % m) % m;
        a = (a % m * a % m) % m;
        b = b >> 1;
    }
    return res;
}
void solve(int T)
{
    int n, k; cin >> n >> k;
    int ans = 0, cnt = 0;
    while (k > 0) {
        int d = k % 2;
        if (d) ans = (ans % mod + fastPower(n, cnt)) % mod;
        cnt++;
        k = k / 2;
    }
    cout << ans << nl;
}
```

### Editorial

```
The problem is the same as finding the k-th number that in base n has only zeros and ones.
So you can write k in binary system and instead of powers of 2 add powers of n.
```

# Finding maximum 'k' such that its modulus with each array element is same

```
Step 1. Find out the difference 'd' between maximum and minimum element of the array
Step 2. Find out all the divisors of 'd'
Step 3. For each divisor check if arr[i]%divisor(d) is same or not .if it is same print it.
```

### Code

```
int printEqualModNumbers (vi &arr, int n)
{
    // sort the numbers
    sort(all(arr));

    // max difference will be the difference between
    // first and last element of sorted array
    int d = arr[n - 1] - arr[0];

    // Case when all the array elements are same
    if (d == 0) {
        return -1;
    }

    int ans = 1;
    vector <int> v;
    for (int i = 1; i * i <= d; i++)
    {
        if (d % i == 0)
        {
            v.push_back(i);
            if (i != d / i)
                v.push_back(d / i);
        }
    }
    // cout << v << nl;
    for (int i = 0; i < v.size(); i++)
    {
        int temp = ((arr[0] % v[i]) + v[i]) % v[i];
        int j;
        for (j = 1; j < n; j++)
            if (((arr[j] % v[i]) + v[i]) % v[i] != temp)
                break;
        if (j == n) ans = max(ans, v[i]);
        // cout << v[i] <<" ";
    }
    return ans;
}
```

# Swapping Type

Hemose has an array of n integers. He wants Samez to sort the array in the non-decreasing order. Since it would be a too easy problem for Samez, Hemose allows Samez to use only the following operation:

Choose indices i and j such that 1≤i,j≤n, and |i−j|≥x. Then, swap elements ai and aj.

Can you tell Samez if there's a way to sort the array in the non-decreasing order by using the operation written above some finite number of times (possibly 0)?

### Editorial

```
The answer is always "YES" If n≥2∗x because you can reorder the array as you want.

Otherwise, You can swap the first n−x elements and the last n−x elements, so you can reorder them as you want but the rest have to stay in their positions in the sorted array.

So if elements in the subarray [n−x+1,x] in the original array are in their same position after sorting the array then the answer is YES, otherwise NO.
```

### Code

```
void solve(int T)
{
    int n, x; cin >> n >> x;
    vi a(n); cin >> a;
    if (2 * x <= n) cout << "YES\n";
    else {
        vi cur;
        for (int i = n - x; i < x; i++) {
            cur.pb(a[i]);
        }
        sort(all(a));
        // cout << cur << nl;
        int k = 0;
        for (int i = n - x; i < x; i++) {
            if (a[i] != cur[k++]) {
                cout << "NO\n";
                return;
            }
        }
        cout << "YES\n";
    }
}

```

# XOR of first n natural number

```
1- Find the remainder of n by moduling it with 4.
2- If rem = 0, then xor will be same as n.
3- If rem = 1, then xor will be 1.
4- If rem = 2, then xor will be n+1.
5- If rem = 3 ,then xor will be 0.
```

# To find k such that it minimises the maximum absolute difference between k and all other values.

The best k is equal to (minimum_value_of_all_the_values + maximum_value_of_all_the_values) / 2.

# Finding superior among n in O(n)

```
https://codeforces.com/problemset/problem/1552/B
```

## Editorial

```
First of all, observe that athlete i is superior to athlete j if and only if athlete j is not superior to athlete i.

The issue is, of course, that we cannot iterate over all pairs of athletes as there are (n2)=O(n2) pairs, which is too much to fit in the time limit.

Notice that there can be at most one athlete who is likely to get the gold medal (if there were 2, one would not be superior to the other which is a contradiction).

Let us describe the algorithm. We iterate over the athletes from 1 to n, keeping a possible winner w.

When we process i, we check whether w is superior to i. In that case, clearly i is not the one who is likely to get the gold medal and we do nothing. On the other hand, if i is superior to w, we deduce that w cannot be the athlete who is likely to get the gold medal. In this case, we assign w:=i and we proceed.

Notice that, when we have finished processing athletes, if there is an athlete superior to everyone else it is for sure w. Finally, we check whether w is superior to everyone else or not.
```

# Keep in mind

```
1. Let suppose a number x, if we take Bitwise & of x with another number y, the resultant will be less than or equal to x i.e x&y≤ x.
2. a + b = a ^ b + 2 * (a & b).
3. how many ways are there to find a pair of non-negative integers whose sum is n? There are clearly n+1 ways: n+0,(n−1)+1,(n−2)+2,…,0+n.
```
