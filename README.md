# Water-Jug-problem-using-BFS
Water Jug problem using BFS

Problem link : https://www.geeksforgeeks.org/water-jug-problem-using-bfs/

Basically at any state (X,Y) there are 6 possibilities to move, explore all of them like BFS.
I am sharing the coding approach

```cpp
class Item{
    int x;
    int y;
    int step;
    Item(int x,int y,int step){
        this.x = x;
        this.y = y;
        this.step = step;
    }
}
class Solution
{
    public int  minSteps(int m, int n, int d)
    {
        // code here
        Queue<Item> q = new LinkedList<Item>();
        
        q.add(new Item(0,0,0));
        int[][] visited = new int[m+1][n+1];
        while(!q.isEmpty()){
            Item item = q.poll();
            visited[item.x][item.y]=1;
            
            //current state of jugs is x and y;
            if(item.x==d || item.y==d)
             return item.step;
            
            //1. empty the jug 1 and leave jug 2 as it is
            if(visited[0][item.y]!=1){
                visited[0][item.y]=1;
                q.add(new Item(0,item.y,item.step+1));
            }
            //2. empty the jug 2 and leave jug 1 as it is
            if(visited[item.x][0]!=1){
                visited[item.x][0]=1;
                q.add(new Item(item.x,0,item.step+1));
            }
            //3. fill the jug 1 and leave jug 2 as it is
            if(visited[m][item.y]!=1){
                visited[m][item.y]=1;
                q.add(new Item(m,item.y,item.step+1));
            }
            //4. fill the jug 2 and leave jug 1 as it is
            if(visited[item.x][n]!=1){
                visited[item.x][n]=1;
                q.add(new Item(item.x,n,item.step+1));
            }
            //5. tranfer the jug1 contents into jug 2
            if(item.y < n){
             //tranfer possible
              int leftOutJug2 = n-item.y;
              
              int val1  = item.x-leftOutJug2;
              if(val1==0){
                  if(visited[0][n]!=1){
                     visited[0][n]=1;
                     q.add(new Item(0,n,item.step+1)); 
                  }
              }
              else if(val1 > 0){
                    if(visited[val1][n]!=1){
                        visited[val1][n]=1;
                        q.add(new Item(val1,n,item.step+1));
                    }
              }                                         
              else{
                  //val1 < 0
                  if(visited[0][item.y+item.x]!=1){
                     visited[0][item.y+item.x]=1; 
                     q.add(new Item(0,item.x+item.y,item.step+1));
                  }
              }
            }
            //6. tranfer the jug2 contents into jug 1
            if(item.x < m){
             //tranfer possible
              int leftOutJug2 = m-item.x;
              
              int val1  = item.y-leftOutJug2;
              if(val1==0){
                  if(visited[m][0]!=1){
                     visited[m][0]=1;
                     q.add(new Item(m,0,item.step+1)); 
                  }
              }
              else if(val1 > 0){
                    if(visited[m][val1]!=1){
                        visited[m][val1]=1;
                        q.add(new Item(m,val1,item.step+1));
                    }
              }                                         
              else{
                  //val1 < 0
                  if(visited[item.y+item.x][0]!=1){
                     visited[item.y+item.x][0]=1; 
                     q.add(new Item(item.x+item.y,0,item.step+1));
                  }
              }
            }
            
        }
        
        return -1;
        
    }
}

```

Time Complexity : O(M * N)
Space Complexity : O(M * N)
