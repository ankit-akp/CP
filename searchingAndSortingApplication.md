# Binary Search

Binary Search: Search in a sorted array by repeatedly dividing the search interval in half.

```
#include <bits/stdc++.h>
using namespace std;

// A iterative binary search function. It returns
// location of x in given array arr[l..r] if present,
// otherwise -1
int binarySearch(int arr[], int l, int r, int x)
{
	while (l <= r) {
		int m = l + (r - l) / 2;

		// Check if x is present at mid
		if (arr[m] == x)
			return m;

		// If x greater, ignore left half
		if (arr[m] < x)
			l = m + 1;

		// If x is smaller, ignore right half
		else
			r = m - 1;
	}

	// if we reach here, then element was
	// not present
	return -1;
}

int main(void)
{
	int arr[] = { 2, 3, 4, 10, 40 };
	int x = 10;
	int n = sizeof(arr) / sizeof(arr[0]);
	int result = binarySearch(arr, 0, n - 1, x);
	(result == -1) ? cout << "Element is not present in array"
				: cout << "Element is present at index " << result;
	return 0;
}

```

## Note

- Agr jo ans hume nikalna h uska range pta ho ki ans [l,r] given range me hi lie krega to ek baar bianry search dimag me aana chahiye.
  Ye check kr lena chahiye ki kya main range ko chota kr sakta hu ki nahi. Agr kr sakta hu to binary search try kr lena chahiye.
- lower_bound() on vector of pairs: By default it will do searching on first element of pair.
  Eg. int pos = lower_bound(all(a), pii(x, -1)) - a.begin();

# Aggressive Cow Problem

```
#include<bits/stdc++.h>
using namespace std;
bool check(vector<int>&a ,int n,int d,int c){
    int prv=a[0];
    int i=1;
    c--;
    while(i<n){
        if(a[i]-prv>=d){
            prv=a[i];
            c--;
            if(c==0) return true;
        }
        i++;
    }
    return false;
}
int main(){
    int t; cin>>t;
    while(t--){
        int n,c; cin>>n>>c;
        vector<int>a(n);
        for(int i=0; i<n; i++) cin>>a[i];
        sort(a.begin(),a.end());
        int d=a[n-1]-a[0];
        int ans=0;
        int i=0,j=d;
        while(i<=j){
            int mid=i+(j-i)/2;
            if(check(a,n,mid,c)){
                ans=mid;
                i=mid+1;
            }
            else j=mid-1;
        }
        cout<<ans<<endl;
    }
    return 0;
}
```

# MergeSort

Merge Sort is a Divide and Conquer algorithm. It divides the input array into two halves, calls itself for the two halves, and then merges the two sorted halves. The merge() function is used for merging two halves.

```
#include<bits/stdc++.h>
using namespace std;
void merge(vector<int>&arr,int s,int mid,int e){
    int n1=mid-s+1,n2=e-mid;
    vector<int>a(n1),b(n2);
    for(int i=0; i<n1; i++) a[i]=arr[s+i];
    for(int i=0; i<n2; i++) b[i]=arr[mid+1+i];
    int i=0,j=0,k=s;
    while(i<n1 and j<n2){
        if(a[i]<b[j]) arr[k++]=a[i++];
        else arr[k++]=b[j++];
    }
    while(i<n1) arr[k++]=a[i++];
    while(j<n2) arr[k++]=b[j++];
}
void mergesort(vector<int>&a ,int s,int e){
    if(s>=e) return;
    int mid=s+(e-s)/2;
    mergesort(a,s,mid);
    mergesort(a,mid+1,e);
    merge(a,s,mid,e);
}
int main(){

    int n; cin>>n;
    vector<int>a(n);
    for(int i=0; i<n; i++) cin>>a[i];
    mergesort(a,0,n-1);
    for(int i=0; i<n; i++) cout<<a[i]<<" ";
}

```

## Note

- Hum mergesort ko basically waha use krenge jaha pe array ko do part me divide krke kuch conditons lga ke hum problem ko solve kr paa rahe honge.

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

# Murder

Once detective Saikat was solving a murder case. While going to the crime scene he took the stairs and saw that a number is written on every stair. He found it suspicious and decides to remember all the numbers that he has seen till now. While remembering the numbers he found that he can find some pattern in those numbers. So he decides that for each number on the stairs he will note down the sum of all the numbers previously seen on the stairs which are smaller than the present number. Calculate the sum of all the numbers written on his notes diary.

## Sample Input

```
1
5
1 5 3 6 4
```

## Sample Output

```
15
```

## Explanation

```
For the first number, the contribution to the sum is 0.
For the second number, the contribution to the sum is 1.
For the third number, the contribution to the sum is 1.
For the fourth number, the contribution to the sum is 9 (1+5+3).
For the fifth number, the contribution to the sum is 4 (1+3).
Hence the sum is 15 (0+1+1+9+4).
```

## Code

```
#include<bits/stdc++.h>
using namespace std;
#define int long long

int merge(vector<int>&arr ,int s,int mid,int e){
    int n1=mid-s+1,n2=e-mid;
    vector<int>a(n1),b(n2);
    for(int i=0; i<n1; i++) a[i]=arr[s+i];
    for(int i=0; i<n2; i++) b[i]=arr[mid+1+i];
    int i=0,j=0,k=s,ans=0;
    while(i<n1 and j<n2){
        if(a[i]<b[j]){
            ans+=(n2-j)*a[i];
            arr[k++]=a[i++];
        }
        else arr[k++]=b[j++];
    }
    while(i<n1) arr[k++]=a[i++];
    while(j<n2) arr[k++]=b[j++];
    return ans;
}

int mergesort(vector<int>&a,int s,int e){
    if(s>=e) return 0;
    int mid=s+(e-s)/2;
    int ans=0;
    ans+=mergesort(a,s,mid);
    ans+=mergesort(a,mid+1,e);
    ans+=merge(a,s,mid,e);
    return ans;
}
int32_t main(){
   int t; cin>>t;
    while(t--){
        int n; cin>>n;
        vector<int>a(n);
        for(int i=0; i<n; i++) cin>>a[i];
        cout<<mergesort(a,0,n-1)<<'\n';
    }
    return 0;
}
```
# QuickSort
```
#include<bits/stdc++.h>
using namespace std;
int partition(vector<int>&a,int s,int e){
    int pivot=a[e];
    int i=s-1;
    for(int j=s; j<=e-1; j++){
        if(a[j]<pivot){
            i++;
            swap(a[i],a[j]);
        }
    }
    swap(a[i+1],a[e]);
    return i+1;
}
void quicksort(vector<int>&a,int s,int e){
    if(s>=e) return;
    int pos=partition(a,s,e);
    quicksort(a,s,pos-1);
    quicksort(a,pos+1,e);
}
int main(){
    
    int t; cin>>t;
    while(t--){
        int n; cin>>n;
        vector<int>a(n);
        for(int i=0; i<n; i++) cin>>a[i];
        quicksort(a,0,n-1);
        for(int i=0; i<n; i++) cout<<a[i]<<" ";
        cout<<endl;
    }
    return 0;
}
```