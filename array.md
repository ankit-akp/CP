# Find the duplicate in an array of N+1 integer

# Sort an array of 0 , 1 and 2 without using extra space or sorting algorithm

# Kadane's Algorithm

# Merge two sorted array without any extra space

# Merge intervals

# Missing and Repeating elements

# Trapping Rain water

# Set Matrix Zero

# Best Time to buy and sell stock

# Rotate Matrix

# Pascal Triangle

# Next Permutation

# Majority Element(>N/2)

# Majority Element(>N/3)

# Unique Path

# Reverse Pair

# Search in 2D Matrix

# Two Sum

# Largest subarray with 0 sum

# Longest consecutive sequence

# Count number of subaaray with given xor

# 3 Sum

# Inversion Count

```
long long merge(long long arr[],int s,int mid,int e){
    int n1=mid-s+1,n2=e-mid;
    long long a[n1];
    long long b[n2];
    for(int i=0; i<n1; i++) a[i]=arr[i+s];
    for(int i=0; i<n2; i++) b[i]=arr[mid+1+i];
    int i=0,j=0,k=s;
    long long ans=0;
    while(i<n1 and j<n2){
        if(a[i]<=b[j]){
            arr[k]=a[i];
            i++;
            k++;
        }
        else{
            ans+=n1-i;
            arr[k]=b[j];
            j++;
            k++;
        }
    }
    while(i<n1){
        arr[k]=a[i];
        i++;
        k++;
    }
    while(j<n2){
        arr[k]=b[j];
        j++;
        k++;
    }
    return ans;
}
long long mergesort(long long arr[],int s,int e){
    if(s>=e) return 0;
    long long ans=0;
    int mid=s+(e-s)/2;
    ans+=mergesort(arr,s,mid);
    ans+=mergesort(arr,mid+1,e);
    ans+=merge(arr,s,mid,e);
    return ans;
}
long long getInversions(long long *arr, int n)
{
   long long ans=mergesort(arr,0,n-1);
    return ans;
}
```
