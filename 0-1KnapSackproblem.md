You are given weights and values of N items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack. Note that we have only one quantity of each item.
In other words, given two integer arrays val[0..N-1] and wt[0..N-1] which represent values and weights associated with N items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of val[] such that sum of the weights of this subset is smaller than or equal to W. You cannot break an item, either pick the complete item or dont pick it (0-1 property).


Top-down :
```cpp
int knapSack(int W, int wt[], int val[], int n) 
    { 
       int arr[n+1][W+1];// static int arr[1002][1002];
        //memset(arr,-1,sizeof(arr));
        // if(arr[n][W]!=-1){
        //     return arr[n][W];
        // }
        for(int i=0;i<n+1;i++){
           for(int j=0;j<W+1;j++){
               if(i==0 || j==0){      // if(n==0 || W==0){
                   arr[i][j]=0;       //     return 0;
               }                      // }
                else if(j<wt[i-1]){        // if(W<wt[n-1])
                    arr[i][j]=arr[i-1][j]; //     return arr[n][W]=knapSack(W,wt,val,n-1);
                }else if(j>=wt[i-1]){      // else
                    arr[i][j]=max(val[i-1]+arr[i-1][j-wt[i-1]],arr[i-1][j]);//     return arr[n][W]=max(val[n-1]+knapSack(W-wt[n-1],wt,val,n-1),knapSack(W,wt,val,n-1));
                }
               
           }
       }
       return arr[n][W];
    }
```


Recursive and Memoisation :
```cpp
int knapSack(int W, int wt[], int val[], int n) 
    { 
      static int arr[1002][1002];
      memset(arr,-1,sizeof(arr));
        if(arr[n][W]!=-1){
             return arr[n][W];
         }
         if(n==0 || W==0){
            return 0;
          }
        if(W<wt[n-1]){
               return arr[n][W]=knapSack(W,wt,val,n-1);
          }else{
              return arr[n][W]=max(val[n-1]+knapSack(W-wt[n-1],wt,val,n-1),knapSack(W,wt,val,n-1));
            }
        }
```
