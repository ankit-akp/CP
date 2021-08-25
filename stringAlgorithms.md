# KMP ALGORITHM

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

// Longest Prefix which is also a suffix
vi getLps(string pattern) {
    int len = pattern.length();
    vi lps(len);
    lps[0] = 0;
    int i = 1, j = 0;
    while (i < len) {
        if (pattern[i] == pattern[j]) {
            lps[i] = j + 1;
            j++;
            i++;
        }
        else {
            if (j != 0) {
                j = lps[j - 1];
            }
            else {
                lps[i] = 0;
                i++;
            }
        }
    }
    return lps;
}
bool kmpSearch(string text, string pattern) {
    int lenText = text.length();
    int lenPat = pattern.length();
    int i = 0, j = 0;
    vi lps = getLps(pattern);
    while (i < lenText and j < lenPat) {
        if (text[i] == pattern[j]) {
            i++;
            j++;
        }
        else {
            if (j != 0) j = lps[j - 1];
            else i++;
        }
    }
    if (j == lenPat) return true;
    return false;
}
void solve() {
    string text, pattern;
    cin >> pattern >> text;
    if (kmpSearch(text, pattern)) cout << "Yes\n";
    else cout << "No\n";
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

# Z ALGORITHM

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

//Longest substring jo ki prefix ke equal h
void buildZ(vi &z, string &str) {
    int l = 0, r = 0, n = str.length();
    for (int i = 1; i < n; i++) {
        if (i > r) {
            l = i, r = i;
            while (r < n and str[r - l] == str[r]) r++;
            z[i] = r - l;
            r--;
        }
        else {
            int k = i - l;
            if (z[k] <= r - i) z[i] = z[k];
            else {
                l = i;
                while (r < n and str[r - l] == str[r]) r++;
                z[i] = r - l;
                r--;
            }
        }
    }
}
void solve() {
    string text, pattern;
    cin >> pattern >> text;
    string str = pattern + "$" + text;
    int n = str.length();
    vi z(n, 0);
    buildZ(z, str);
    for (int i = 0; i < n; i++) {
        if (z[i] == pattern.length()) {
            //This means pattern is present at index i-pattern.length()-1
            cout << i - pattern.length() - 1 << nl;
        }
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
