# 134 Gas Station

1. 只要所有的油能够跑完所有的路，那么就存在解

2. 例

	```
  g0 g1 g2 g3 g4 g5 //站内油量
  c0 c1 c2 c3 c4 c5 //路程耗油量
  ```
  
  如果`g0`不能够到`g3`，那么必有
  
  ```
  g0-c0>=0 ......(1)
  g0-c0+g1-c1>=0 ......(2)
  g0-c0+g1-c1+g2-c2<=0 ......(3)
  (3)-(1) :g1-c1+g2-c2<=0
  (3)-(2) :g2-c2<=0
  ...
  可以得到之前的任何一个站点都不能到g3
  ```
  
  如果g3能够到达g1，那么必有
  
  ```
  g3-c3>=0
  g3-c3+g4-c4>=0
  g3-c3+g4-c4+g5-c5>=0
  ```
  
  因为有
  
  ```
  g0-c0+g1-c1+g2-c2+g3-c3+g4-c4+g5-c5>=0
  g3-c3+g4-c4+g5-c5+g0-c0+g1-c1+g2-c2>=0
  ```
  
  那么当车🚗从`g3`把余油带回起始点，车就能够再次回到`g3`
  
3. 官方方法

   ```c++
   class Solution {
   public:
       int canCompleteCircuit(vector<int>& g, vector<int>& cost) {
           int n=g.size();
           int ans=0,gas=0,total=0;
           vector<int> one(n,INT_MAX);
           for(int i=0;i<n;i++){
               gas+=g[i];
               gas-=cost[i];
               total+=g[i]-cost[i];
               if(gas<0){
                   ans=i+1;
                   gas=0;
               }
           }
           if(total>=0)return ans;
           return -1;
       }
   };
   ```

   

