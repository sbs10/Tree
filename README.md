# Tree
DataStructure
Source:https://www.hackerrank.com/challenges/swap-nodes-algo
Swap operation: 
           Given a tree and a integer, K, we have to swap the subtrees of all the nodes who are at depth h, where h ∈ [K, 2K, 3K,...].

You are given a tree of N nodes where nodes are indexed from [1..N] and it is rooted at 1. You have to perform T swap operations on it,
and after each swap operation print the inorder traversal of the current state of the tree.

Input Format 
First line of input contains N, number of nodes in tree. 
Then N lines follow. Here each of ith line (1 <= i <= N) contains two integers, a b, 
where a is the index of left child, and b is the index of right child of ith node. 
-1 is used to represent null node. 
Next line contain an integer, T. Then again T lines follows. Each of these line contains an integer K.

Output Format 
For each K, perform swap operation as mentioned above and print the inorder traversal of the current state of tree.

Constraints 
1 <= N <= 1024 
1 <= T <= 100 
1 <= K <= N 
Either a = -1 or 2 <= a <= N 
Either b = -1 or 2 <= b <= N 
Index of (non-null) child will always be greater than that of parent.

#code

#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

struct node{
    int left;
    int right;
}nn;
vector< node >v;

void swap(int root, int h, int k)
{
    
    if(root == -1) return;
    if(h%k==0)
      {
        int temp=v[root].left;
        v[root].left=v[root].right;
        v[root].right=temp;
      }
    swap(v[root].left,h+1,k);
    swap(v[root].right,h+1,k);
}

void inorder (int root)
{
    if(root == -1) return;
    inorder(v[root].left);
    cout<<root<<" ";
    inorder(v[root].right);
}

int main() {
    
    int n;
    cin>>n;
    nn.left=nn.right=0;
    v.push_back(nn);
    for(int i=1;i<=n;i++)
       {
          cin>>nn.left>>nn.right;
          v.push_back(nn); 
       }
    int q,k;
    cin>>q;
    while(q--)
        {
         cin>>k;
         swap(1,1,k);
         inorder(1);
         cout<<endl;
        }
    return 0;
}
