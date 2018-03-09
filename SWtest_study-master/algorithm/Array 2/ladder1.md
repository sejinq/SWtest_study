# Array2

## Ladder 1

- Input

  test case index

  100x100 map 배열 값 (0 또는 1, 도착 지점은 2)

- Output

  값이 2인 지점으로 내려가는 사다리 출발 지점

>풀이 방법
>
>도착지점이 정해져 있는 길찾기와 유사
>
>입력 받을 시 미리 값이 2인 지점을 알아 놓은 다음
>
>해당 지점부터 맨위의 지점까지 거슬로 올라간다.
>
>첫번째 row에 도달할 때 그 지점이 출발 지점
>
>위로 올라가는 것보다 왼쪽, 오른쪽 방향으로 전진하는 것에 우선순위를 둔다

**point : row와 column 값이 혼동될 수 있음. (좌표의 x,y와 다름)**

```java
import java.io.*;
import java.util.*;
 
class Solution{
    public static int[][] arr = new int[100][100];
    //해당 지점을 방문했는지를 검사하는 배열
    public static boolean[][] visit = new boolean[100][100];
    public static int answer;
    //움직일 수 있는 방향. right, left, up(거슬러 올라가기 때문)
    public static int[] dx = {0, 0, -1};
    public static int[] dy = {1, -1, 0};
    //배열의 범위에서 벗어나지 않는가를 체크하는 함수 
    public static boolean check(int x, int y){
        if(x>=100||x<0||y>=100||y<0) return false;
        return true;   
    }
    public static void dfs(int ax, int ay){
        visit[ax][ay] = true; //방문
        //row=0, 출발 지점까지 거슬러 올라왔다는 것으로 종료
        if(ax==0){
            //row가 일 때의 column값이 출발지점
            answer = ay; return;
        }
        boolean up = false; //right, left이동에 우선순위를 두기 위한 제어 변수
        for(int i=0;i<3;i++){ //움직일 수 있는 방향으로 움직임
            int tempx = ax+dx[i];
            int tempy = ay+dy[i];
            if(i==2&&up) continue; //up일 때는 앞서 좌, 우로 먼저 이동했었는지를 확인. 만약 좌, 우값으로 이동했었더라면 진행하지 말아야한다.
            if(check(tempx, tempy)&&arr[tempx][tempy]==1&&!visit[tempx][tempy]){
                dfs(tempx, tempy); //재귀적으로 전진
                up = true;
            }                
        }
         
    }
  //bufferedwriter는 입출력에 예외 처리를 해 주어야함
    public static void main(String[] args) throws IOException {
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        Scanner scn = new Scanner(System.in);
         
        for(int loop=0;loop<10;loop++){
            int index = scn.nextInt();
            int ax=0, ay=0;
            for(int i=0;i<100;i++){
                for(int j=0;j<100;j++){
                    arr[i][j] = scn.nextInt();
                    //입력시 찾아야할 지점 위치를 미리 기억해둔다
                    if(arr[i][j]==2){
                        ax = i;
                        ay = j;
                    }
                    //입력과 동시에 visit 배열 초기화. 
                    visit[i][j] = false;
                }
            }
          //목적 값부터 탐색 시작. 거슬러 올라가기
            dfs(ax, ay);
            bw.append("#"+index+" "+answer+"\n");
        }
        bw.flush();
        bw.close();
    }
}
```



