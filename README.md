# Leetcode---2658
Maximum Number of Fish in a Grid
//CODE IN C++
class Solution {
public:
    const int dx[4]={-1,0,0,1};
    const int dy[4]={0,-1,1,0};
 
    int dfs(int i,int j,int r,int c,vector<vector<int>>&vis,vector<vector<int>>& grid){
        if(vis[i][j] || i>=r || j>=c || i<0 || j<0)return 0;
        vis[i][j]=1;
           int ans=0;
           for(int k=0;k<4;++k){
               int x=dx[k]+i;
               int y=dy[k]+j;
               if(x<r && x>=0 && y<c && y>=0 && !vis[x][y] && grid[x][y]){
                  ans+=grid[x][y]+dfs(x,y,r,c,vis,grid);      
 
               }
 
           }          
        return ans;
 
 
    }
    int findMaxFish(vector<vector<int>>& grid) {
        int r=grid.size(),c=grid[0].size();
        vector<vector<int>>vis(r,vector<int>(c,0));
 
        int maxi=0;
        for(int i=0;i<r;++i){
            for(int j=0;j<c;++j){
                 if(!vis[i][j] && grid[i][j]){
                     maxi=max(  grid[i][j]+dfs(i,j,r,c,vis,grid),maxi);
                 }
            }
        }
 
        return maxi;
 
    }
};
