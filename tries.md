# Maximum XOR of Two Numbers in an Array
Given an integer array nums, return the maximum result of nums[i] XOR nums[j], where 0 <= i <= j < n.  
### Constraints
```
1 <= nums.length <= 2 * 105
0 <= nums[i] <= 231 - 1
```
### Code
```
class trieNode{
public:
    trieNode* left;
    trieNode* right;
};
void insert(int n,trieNode* root){
    trieNode* cur=root;
    for(int i=31; i>=0; i--){
        int b=(n>>i)&1;
        if(b==0){
            if(!cur->left) cur->left=new trieNode();
            cur=cur->left;
        }
        else{
            if(!cur->right) cur->right=new trieNode();
            cur=cur->right;
        }
    }
}
int findMaximumXorPair(trieNode* root,vector<int> &a,int n){
    int max_xor=INT_MIN;
    for(int i=0; i<n; i++){
        int value=a[i];
        int cur_xor=0;
        trieNode* cur=root;
        for(int j=31; j>=0; j--){
            int b=(value>>j)&1;
            if(b==0){
                if(cur->right){
                    cur_xor+=pow(2,j);
                    cur=cur->right;
                }
                else cur=cur->left;
            }
            else{
                if(cur->left){
                    cur_xor+=pow(2,j);
                    cur=cur->left;
                }
                else cur=cur->right;
            }
        }
        max_xor=max(max_xor,cur_xor);
    }
    return max_xor;
}
int findMaximumXOR(vector<int>& nums) {
        trieNode* root=new trieNode();
        for(auto i:nums) insert(i,root);
        int n=nums.size();
        return findMaximumXorPair(root,nums,n);
        
    }
```
# Maximum XOR Subarray
Given an array of N integers, find the subarray whose XOR is maximum.  
### Input Format
```
First line of input contains an integer N, representing number of elements in array.
Next line contains N space-separated integers.
```
### Constraints
```
1 <= N <= 10^6
1 <= A[i] <=10^5 
```
### Output Format
```
Print XOR of the subarray whose XOR of all elements in subarray is maximum over all subarrays.
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
class trieNode {
public:
    trieNode* left;
    trieNode* right;
};
void insert(int n, trieNode* root) {
    trieNode* cur = root;
    for (int i = 31; i >= 0; i--) {
        int b = (n >> i) & 1;
        if (b == 0) {
            if (!cur->left) cur->left = new trieNode();
            cur = cur->left;
        }
        else {
            if (!cur->right) cur->right = new trieNode();
            cur = cur->right;
        }
    }
}
int query(trieNode* root, int value) {
    int res = 0;
    trieNode*cur = root;
    for (int i = 31; i >= 0; i--) {
        int b = (value >> i) & 1;
        if (b == 0) {
            if (cur->right) {
                cur = cur->right;
                res += pow(2, i);
            }
            else cur = cur->left;
        }
        else {
            if (cur->left) {
                cur = cur->left;
                res += pow(2, i);
            }
            else cur = cur->right;
        }
    }
    return res;
}
void solve() {
    int n; cin >> n;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    trieNode* root = new trieNode();
    int preXor = 0;
    int ans = INT_MIN;
    for (int i = 0; i < n; i++) {
        preXor = preXor ^ a[i];
        insert(preXor, root);
        ans = max(ans, query(root, preXor));
    }
    //ans = max(ans, query(root, preXor));
    cout << ans << nl;
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
# Sub - XOR
Given an array of positive integers, you have to print the number of subarrays whose XOR is less than K. Subarrays are defined as a sequence of continuous elements Ai, Ai + 1, ..., Aj. XOR of a subarray is defined as Ai ^ Ai + 1 ^ ... ^ Aj. Symbol ^ is Exclusive Or.  
### Input Format
```
First line of input contains N and K, space separated.
Second line of input contains N space separated.integers.
```
### Constraints
```
1 ≤ N ≤ 10^5
1 ≤ A[i] ≤ 10^5
1 ≤ K ≤ 10^6
```
### Output Format
```
For each test case, print the required answer.
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
class trieNode {
public:
    trieNode* left;
    trieNode* right;
    int l = 0, r = 0;
};
void insert(int n, trieNode* root) {
    trieNode* cur = root;
    for (int i = 31; i >= 0; i--) {
        int b = (n >> i) & 1;
        if (b == 0) {
            cur->l++;
            if (!cur->left) cur->left = new trieNode();
            cur = cur->left;
        }
        else {
            cur->r++;
            if (!cur->right) cur->right = new trieNode();
            cur = cur->right;
        }
    }
}
int query(trieNode* root, int value, int k) {
    int res = 0;
    if (root == NULL) return res;
    int kb, ib;
    trieNode* cur = root;
    for (int i = 31; i >= 0; i--) {
        kb = (k >> i) & 1;
        ib = (value >> i) & 1;
        if (kb) {
            if (ib) {
                res += cur->r;
                if (cur->left) cur = cur->left;
                else return res;
            }
            else {
                res += cur->l;
                if (cur->right) cur = cur->right;
                else return res;
            }
        }
        else {
            if (ib) {
                if (cur->right) cur = cur->right;
                else return res;
            }
            else {
                if (cur->left) cur = cur->left;
                else return res;
            }
        }
    }
    return res;
}
void solve() {
    int n, k; cin >> n >> k;
    vi a(n);
    for (int i = 0; i < n; i++) cin >> a[i];
    trieNode* root = new trieNode();
    int preXor = 0;
    int ans = 0;
    insert(preXor, root);
    for (int i = 0; i < n; i++) {
        preXor = preXor ^ a[i];
        ans += query(root, preXor, k);
        insert(preXor, root);

    }
    //ans = max(ans, query(root, preXor));
    cout << ans << nl;
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
# Search Engine
Let us see how search engines work. Consider the following simple auto complete feature. When you type some characters in the text bar, the engine automatically gives best matching options among it's database. Your job is simple. Given an incomplete search text, output the best search result.  
Each entry in engine's database has a priority factor attached to it. We consider a result / search suggestion best if it has maximum weight and completes the given incomplete search query. For each query in the input, print the maximum weight of the string in the database, that completes the given incomplete search string. In case no such string exists, print -1.  
### Input Format
```
First line contains two integers n and q, which represent number of database entries and number of search queries need to be completed. 
Next n lines contain a string s and an integer weight, which are the database entry and it's corresponding priority.
Next q lines follow, each line having a string t, which needs to be completed.
```
### Constraints
```
1 ≤ n, weight, len(s), len(t) ≤ 10^6
1 ≤ q ≤ 10^5
Total length of all strings in database entries ≤ 10^6
Total length of all query strings ≤ 10^6
```
### Output Format
```
Output q lines, each line containing the maximum possible weight of the match for given query, else -1, in case no valid result is obtained.
```
### Code
```

```
# Order
- Maximum XOR of Two Numbers in an Array
- Maximum XOR Subarray
- Sub - XOR
- Search Engine