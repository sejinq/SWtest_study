# Array 2

## Ladder 2

- Input

  testcase index

  100x100 map array(0 or 1)

- Output

  최단 거리로 마지막 row에 도달하는 사다리 시작 지점

> 풀이방법
>
> 



```java
import java.io.*;
import java.util.*;
  
class Solution{
    public static int[][] arr = new int[100][100];
    public static boolean[][] visit = new boolean[100][100];
    public static int answer=0;
    public static int min=99999;
    public static int[] dx = {0, 0, 1};
    public static int[] dy = {1, -1, 0};
     
    public static boolean check(int x, int y){
        if(x>=100||x<0||y>=100||y<0) return false;
        return true;   
    }
    public static void dfs(int ax, int ay, int length, int startpoint){
        visit[ax][ay] = true; length++;
        if(ax==99){
            if(min >= length ){
                min = length;
                answer = startpoint;
            }
            return;
        }
        boolean down = false;
        for(int i=0;i<3;i++){
            int tempx = ax+dx[i];
            int tempy = ay+dy[i];
            if(i==2&&down) continue;
            if(check(tempx, tempy)&&arr[tempx][tempy]==1&&!visit[tempx][tempy]){
                dfs(tempx, tempy, length, startpoint);
                down = true;
            }                
        }
    }
    public static void main(String[] args) throws IOException {
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        Scanner scn = new Scanner(System.in);
        for(int loop=0;loop<10;loop++){
            int index = scn.nextInt();
            min = 99999;
            for(int i=0;i<100;i++){
                for(int j=0;j<100;j++){
                    arr[i][j] = scn.nextInt();
                }
            }
            for(int i=0;i<100;i++){
                if(arr[0][i]==1){
                    for(int j=0;j<100;j++) Arrays.fill(visit[j], false);
                    dfs(0, i, 0, i);
                }
            }
            bw.append("#"+index+" "+answer+"\n");
        }
        bw.flush();
        bw.close();
    }
}
```

