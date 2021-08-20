# N Queen

```
#include<bits/stdc++.h>
using namespace std;
map<int,int> row,column,d1,d2;
void solve(vector<vector<int>> &a,int n,int idx){
    if(idx==n){
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++) cout<<a[i][j]<<" ";
        }
        cout<<endl;
        return;
    }

    for(int i=0; i<n; i++){
        if(column[i]!=1 and row[idx]!=1 and d1[i+idx]!=1 and d2[n-1+i-idx]!=1){
            a[idx][i]=1;
            row[idx]=1;
            column[i]=1;
            d1[i+idx]=1; //(col+row)
            d2[n-1+i-idx]=1; //(n-1+col-row)

            solve(a,n,idx+1);

            a[idx][i]=0;
            row[idx]=0;
            column[i]=0;
            d1[i+idx]=0;
            d2[n-1+i-idx]=0;

        }
    }
}
int main(){

    int n; cin>>n;
    vector<vector<int>>a(n,vector<int>(n,0));

    solve(a,n,0);
    return 0;
}
```

# Sodoku Solver

```
#include<bits/stdc++.h>
using namespace std;
bool check(vector<vector<int>> &a,int row,int col,int k){
    for(int i=0; i<9; i++){
        if(a[row][i]==k) return false;
        if(a[i][col]==k) return false;
        if(a[3*(row/3)+i/3][3*(col/3)+i%3]==k) return false;
    }
    return true;
}
bool solve(vector<vector<int>> &a){
    for(int i=0; i<9; i++){
        for(int j=0; j<9; j++){
            if(a[i][j]==0){
                for(int k=1; k<10; k++){
                    if(check(a,i,j,k)){
                        a[i][j]=k;
                        if(solve(a)) return true;
                        else a[i][j]=0;
                    }
                }
                return false;
            }
        }
    }
    return true;
}
int main(){

    vector<vector<int>>a(9,vector<int>(9,0));
    for(int i=0; i<9; i++){
        for(int j=0; j<9; j++) cin>>a[i][j];
    }
    if(solve(a)) cout<<"true";
    else cout<<"false";
    return 0;
}
```

# Rat in a Maze

```
/*
	Note:
	To get all the test cases accepted, make recursive calls in following order: Top, Down, Left, Right.
	This means that if the current cell is (x, y), then order of calls should be: top cell (x-1, y),
	down cell (x+1, y), left cell (x, y-1) and right cell (x, y+1).
*/
#include<bits/stdc++.h>
using namespace std;
vector<vector<int>>vis(20,vector<int>(20,0));
int dx[]={-1,1,0,0};
int dy[]={0,0,-1,1};
void solve(vector<vector<int>>&a,int n, int row,int col){
    if(row==n-1 and col==n-1){
        vis[row][col]=1;
        for(int i=0; i<n; i++){
        for(int j=0; j<n; j++) cout<<vis[i][j]<<" ";
    	}
        vis[row][col]=0;
        cout<<endl;
        return;
    }
    for(int i=0; i<4; i++){
        if(row+dx[i]>=0 and row+dx[i]<n and col+dy[i]>=0 and col+dy[i]<n and a[row+dx[i]][col+dy[i]]==1
          and vis[row+dx[i]][col+dy[i]]==0){
            vis[row][col]=1;
            solve(a,n,row+dx[i],col+dy[i]);
            vis[row][col]=0;
        }
    }
}
int main() {

	int n; cin>>n;
    vector<vector<int>>a(n,vector<int>(n,0));
    for(int i=0; i<n; i++){
        for(int j=0; j<n; j++) cin>>a[i][j];
    }

    solve(a,n,0,0);
	return 0;
}

```

# Combinational sum 1

# Combinational sum 2

# subset sum 1

# subset sum 2

# Permutation of an array
