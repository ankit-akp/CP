# Sieve of Eratosthenes

Time Complexity: O(Nlog(log(N)))  
Given a number n, print all primes smaller than or equal to n.

```
vector<bool> prime(1000001, true);
    prime[0] = prime[1] = false;
    for (int i = 2; i * i <= 1000000; i++) {
        if (prime[i]) {
            for (int p = i * i; p <= 1000000; p += i)
                prime[p] = false;
        }
    }
    //Now in prime array only prime number is marked as true
```

# Smallest prime factor of n numbers

```
    spf[1] = 1;
    for (int i = 2; i <= 1000000; i ++) spf[i] = i;
    for (int i = 4; i <= 1000000; i += 2) spf[i] = 2;
    for (int i = 3; i * i <= 1000000; i++) {
        if (spf[i] == i) {
            for (int p = i * i; p <= 1000000; p += i)
                if (spf[p] == p) spf[p] = i;
        }
    }
```

# Count no. of prime divisor of n numbers

Time Complexity:O(Nlog(logN))

```
    vi pf(1000001, 0);
    for (int i = 2; i <= 1000000; i++) {
        if (pf[i] == 0) {
            for (int j = i; j <= 1000000; j+=i) pf[j]++;
        }
    }

```

# Euclid Algorithm

gcd(a,b)=gcd(b,a%b)  
gcd(a,0)=a  
Time Complexity: O(log(max(a,b)))

```
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}
```

# Advanced GCD

Calculate gcd of two integers, one is a little integer and another integer can have 10^4 digits.

```
 int a; cin >> a;
    string b; cin >> b;
    int prv = 0;
    for (int i = 0; i < b.size(); i++) {
        int cur = b[i] - '0';
        prv = ((prv * (10 % a)) % a + cur % a) % a;
    }
    cout << __gcd(a, prv) << nl;
```

# Linear Diophantine eqn

Lets consider an equation ax+by=c where a,b and c is integers.  
x and y will be integer only if gcd(a,b) divides c.

# Extended Euclid Algorithm

Lets consider an equation ax+by=gcd(a,b) then find x and y.

```
int gcd(int a, int b, int &x, int &y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int d = gcd(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return d;
}
void solve() {
    int a, b, x, y;
    cin >> a >> b;
    int g = gcd(a, b, x, y);
    cout << x << " " << y << nl;
}

```

# Multiplicative Modulo Inverse

Multiplicative Modulo Inverse -> (A.B)%m=1 ->(A.B-1)%m=0 -> (A.B-1)=m.q -> (A.B)-m.q=1 -> (A.B)+(m.Q)=1 -> Now according to extended euclid algorithm, this equation will have integral solution only when gcd(A, m) divides 1, i.e. gcd(A, m)==1. Which in turn means that A and m should be Coprime. Hence we can say that, (A.B)+(m.Q)=gcd(A, m).

```
(A*B)%m=1 then B is multiplicative modulo inverse of A.
A and m should be co prime or gcd(A,m)=1.
```

```
int gcd(int a, int b, int &x, int &y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int d = gcd(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return d;
}
int modInv(int a, int b) {
    int x, y;
    int g = gcd(a, b, x, y);
    if(g!=1){
        cout << "NO SOLUTION\n";
        return -1;
    }
    x = (x % b + b) % b;
    return x;
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

# Number of divisor in N!

If a number N is written in the form p1^a.p2^b.p3^c.....pn^k, where a, b, c, ..... , k are non negative integers and p1, p2, p3....pn are prime numbers, then the number N will have exactly `(a+1)*(b+1)*(c+1)....(k+1)` number of divisors.

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
vi spf(1000011, 0);
vi primes;
vector<bool>prime(1000011, true);
void precompute() {
    prime[0] = prime[1] = false;
    for (int i = 2; i * i <= 1000010; i++) {
        if (prime[i]) {
            for (int p = i * i; p <= 1000010; p += i)
                prime[p] = false;
        }
    }
}

void solve() {
    int n; cin >> n;
    int ans = 1;
    for (int i = 2; i <= n; i++) {
        if (prime[i]) {
            int p = i, cnt = 0;
            while (n / p > 0) {
                cnt += n / p;
                p = p * i;
            }
            ans = (ans % mod * ((cnt + 1) % mod)) % mod;
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

# Euler Totient Function for an number

- Φ(n) is the number of m such that, `1 <= m < n` and n and m are coprime that is gcd(m, n)==1.
- `Φ(a.b)=Φ(a)*Φ(b)`, on the condition that a and b are coprime, i.e. gcd(a, b)=1.
- Since every number n can be expressed in the form of its prime factors, i.e. `n=p1^a*p2^b*p3^c.....pt^k`. So according to the property of Euler totient function, we can write `Φ(n)=Φ(p1^a)Φ(p2^b)Φ(p3^c)....Φ(pt^k)`. Now lets talk about Φ(p^a). Here, according to the definition of Euler's Totient function, Φ(p^a) is the number of m such that m and p^a are coprime and m belongs to [1, m). Now, since p is a prime, so p, 2p, 3p, 4p..... up to p^(a-1) are those numbers which are not coprime with p^a. so we can write: Φ(p^a)=p^a-(total elements not coprime to p^a). i.e. Φ(p^a)=p^a-p^{a-1}. hence Φ(p^a)=p^a(1-(1/p)). Finally we can write that, Φ(n)=Φ(p1^a)Φ(p2^b)Φ(p3^c)....Φ(pt^k), which implies `Φ(n)=p1^a(1-(1/p1))*p2^b(1-(1/p2))*p3^c(1-(1/p3)).....pt^k(1-(1/pt))`. and Finally we have `Φ(n)=n*(1-(1/p1))*(1-(1/p2))*(1-(1/p3))*....(1-(1/pt))`, where t is the number of distinct prime factors.
- `LCM(a, n)=(a*n)/GCD(a, n)`
- `GCD(a,n)=GCD(n-a,n)`

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
// vi spf(1000011, 0);
// vi primes;
// vector<bool>prime(1000011, true);
// vvi cpr(100001, vi(1000, 0));
vi pf(1000001, 0);
void precompute() {

}

void solve() {
    int n; cin >> n;
    int ans = n;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            while (n % i == 0) n = n / i;
            ans -= ans / i;
        }
    }
    if (n > 1) ans -= ans / n;
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

# Euler Totient Function for n numbers

```
void phi_1_to_n(int n) {
    vector<int> phi(n + 1);
    phi[0] = 0;
    phi[1] = 1;
    for (int i = 2; i <= n; i++)
        phi[i] = i;

    for (int i = 2; i <= n; i++) {
        if (phi[i] == i) {
            for (int j = i; j <= n; j += i)
                phi[j] -= phi[j] / i;
        }
    }
}
```

# Find pow(a,b) in log(b)

pow(a,n)=1 if n==0  
pow(a,n)=pow(a,n/2)*pow(a,n/2) if n>0 and n is even  
pow(a,n)=pow(a,n-1)*a if n>0 and n is odd

Time Complexity: Log(b)

```
long long fastPower(int a, int b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1) res = res * a;

        a = a * a;
        b = b >> 1;
    }
    return res;
}
```

# Find pow(a,b)%m in log(b)

```
long long fastPower(int a, int b, int m = 1000000007) {
    long long res = 1;
    while (b > 0) {
        if (b & 1) res = (res % m * a % m) % m;

        a = (a % m * a % m) % m;
        b = b >> 1;
    }
    return res;
}
```

# Segmented Sieve

You have to print all primes from given interval.

## Input Format

```
First line of input will contain T(number of test cases), each test case follows as.

On each line are written two integers L and U separated by a blank. L - lower bound of
interval, U - upper bound of interval.
```

## Output Format

```
For each test case output must contain all primes from interval [L; U] in increasing order.
```

## Constraints

```
1  <= T <= 100
1 <= L <= U <= 10^9
0 <= U - L <= 10^5
```

## Sample Input

```
2
2 10
3 7
```

## Sample Output

```
2 3 5 7
3 5 7
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
#define pii pair<int,int>
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(0);                       \
    cout.tie(0);

vi primes;
vector<bool>prime(100001, true);

void precompute() {
    prime[0] = prime[1] = false;
    for (int i = 2; i * i <= 100000; i++) {
        if (prime[i]) {
            for (int j = i * i; j <= 100000; j += i)
                prime[j] = false;
        }
    }
    for (int i = 2; i <= 100000; i++) {
        if (prime[i]) primes.push_back(i);
    }
}


void solve() {
    int l, r; cin >> l >> r;
    vi isPrime(r - l + 1, true);
    for (int i = 0; primes[i]*primes[i] <= r; i++) {
        int cur = primes[i];
        int base = (l / cur) * cur;
        if (base < l) base += cur;
        for (int j = base; j <= r; j += cur) {
            isPrime[j - l] = false;
        }
        if (base == cur) isPrime[base - l] = true;
    }
    if(l==1) isPrime[0]=false;
    for (int i = 0; i <= r - l; i++) {
        if (isPrime[i]) cout << i + l << " ";
    }
    cout << nl;
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
