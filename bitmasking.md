# Left Shift (<<)

- Number << numberOfPlaces => Number\*(2^(numberOfPlaces))
- N << i => N\*(2^i)

# Right Shift (>>)

- Number >> numberOfPlaces => Number/(2^(numberOfPlaces))
- N >> i => floor(N/(2^i))
- In right shift we append 0 in start for positive number and append 1 in start for negative number

# AND (&)

x is a bit(0 or 1)

- x & 1 = x
- x & 0 = 0

# OR (|)

x is a bit(0 or 1)

- x | 1 = 1
- x | 0 = x

# NOT (~)

It flips the bit.

~0 = 1 and ~1=0  
Let x=000010000  
~x=111101111

# XOR (^)

x is a bit(0 or 1)

- x ^ 1 = ~x (Flip the bit)
- x ^ 0 = x

# Check ith bit is set or not

1 << i => 2^i(2 to the power i)  
mask=(1 << i)  
z=N & mask

if z==0 then ith bit is 0  
else ith bit is 1

# Flip a specific bit

mask = (1 << i)  
z=N ^ mask

# Check wether N is power of 2 or not

if N & (N-1) == 0 then N is power of 2  
else N is not power of 2

# Remove all set bit from LSB to i

mask = ~((1 << (i+1))-1)  
ans = N & mask

# Remove all set bit from MSB to i

mask = (1 << i) - 1  
ans = (N & mask)

# XOR of first N natural number

Find the remainder of n by moduling it with 4.  
If rem = 0, then xor will be same as n.  
If rem = 1, then xor will be 1.  
If rem = 2, then xor will be n+1.  
If rem = 3 ,then xor will be 0.

# Count number of set bits in a number

```
1. __builtin_popcount(x): This function is used to count the number of one’s(set bits) in an integer.
2. Similarly you can use __builtin_popcountl(x) & __builtin_popcountll(x) for long and long long data types.
```

# XOR swapping

a = a ^ b  
b = b ^ a  
a = a ^ b

# Note

- N = 0100100 then N-1 => 0100011
- N & (N-1) removes last set bit
