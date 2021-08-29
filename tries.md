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
# Order
- Maximum XOR of Two Numbers in an Array
