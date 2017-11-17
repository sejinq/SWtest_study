# DFS, BFS

### 깊이우선 탐색(Depth First Search)

가능한 가장 깊이 들어갔다가 더 이상 진행되지 않으면 이전 상태로 돌아와서 반복

어떤 정점을 방문하여 확인 후 우선순위가 가장 빠른 하나를 선택해 방문, 더 이상 방문할 곳이 없으면 이전 상태로 돌아온다.**(Back-tracking)**

- 재귀함수의 호출/실행과정과 완전히 같다.
- 전체탐색법


- backtrack : 모든 비선형구조 문제에 대해 적용할 수 있음
  - 스택구조나, 재귀함수를 이용

>인접행렬 구조 사용
>
>```
>bool visited[101];	//방문 체크 배열
>void dfs(int k){
>  for(int i=0;i<=n;i++){
>    if(G[k][i]==1 && !visited[i]){
>      visited[k]=true;
>      dfs(i);
>    }
>  }
>  return; // 더이상 방문할 곳이 없을 때
>}
>```
>
>인접리스트 구조 사용 : 인접행렬보다 빠른 탐색
>
>```c++
>void dfs(int k){
>    cout << "정점"<<k<<"방문"<<endl;
>  for(int i=0;i<G[k].size();i++){
>    if(!visited[G[k][i]]){
>      visited[G[k][i]] = true;
>      dfs(G[k][i]);
>    }
>  }
>  return;
>}
>```

- 두더지굴 문제

  배열의 (0, 0)부터 하나씩 순차탐색 진행

  어떤 위치의 값이 1인 곳이 나타나면 **그 위치를 시작으로 깊이우선 탐색(상, 하, 좌, 우)**을 진행 > 연결된 부분을 counting하고 탐색 했다는 표시로 2,3,4...로 바꿈(visited)

  크기를 저장 시킨 후 sort

  ```c++
  //pair<int, int>의 사용예제
  #include<iostream>
  #include<vector>
  #include<algorithm>
  using namespace std;

  int G[101][101];
  int visited[101];//방문 체크 배열
  int n;
  int m;
  int temp;
  //진행할 수 있는 곳인지 확인하는 함수
  bool safe(int a, int b){
      if(a<=0||a>n||b<=0||b>m){
          return false;
      }
  }
  void dfs(int a, int b, int c){ //(a, b) 위치, c는 굴의 수(카운팅 변수)
     G[a][b] = c;
     temp++;
     //위로 1칸 탐색
     if(safe(a+1, b) && G[a+1][b] == 1)  dfs(a+1, b, c);
     //아래로 1칸 탐색
     if(safe(a-1, b) && G[a-1][b] == 1)  dfs(a-1, b, c);
     //왼쪽으로 1칸 탐색
     if(safe(a, b-1) && G[a][b-1] == 1)  dfs(a, b-1, c);
     //오른쪽으로 1칸 탐색
     if(safe(a, b+1) && G[a][b+1] == 1)  dfs(a, b+1, c);
     
    return; // 더이상 방문할 곳이 없을 때
  }
  int main(){
    int count=2;
    int size[100]={0, };
    cin >> n >> m;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
          cin >> G[i][j];
        }
    }
   for(int i=1;i<=n;i++){
     for(int j=1;j<=m;j++){
       if(G[i][j] == 1){
           dfs(i, j, count);
           size[count] = temp;
           temp =0;
           count++;
       }
     }
    }
    count--;
    sort(size, size+count);
    cout << "두더지 굴의 수 : "<< count-1 <<endl;
    cout << "가장 큰 두더지 굴 : " << size[count] << endl;
    return 0;
  }
  ```

  만약 입력 데이터의 공백이 없을 시 : scanf("%1d", &arr[i]); > 로 한자리씩 입력받으면됨.

  ​

### 너비우선 탐색(Breadth First Search)

가능한 가장 가까운(옆으로) 정점들을 방문 후 진행

큐(queue) 자료구조 이용 - 줄을 세워 차례로 방문(깊이 1애들, 깊이 2 애들...)

- std::queue를 사용할 수 있다.
  - a데이터 삽입 : queue.push(a);
  - 데이터 가져오기 : queue.front();
  - 맨 앞 데이터 삭제 : queue.pop();
  - 크기 : queue.size();
  - 비어있는지 확인 : queue.empty(); // 비어 있을 때 true 반환

인접행렬 사용

```c++
#include<queue>
bool visited[101];
void bfs(int k){ //정점 k부터 탐색 시작
	std::queue<int> Q;
	Q.push(k);
	visited[k] = 1;
	while(!Q.empty()){
      //더이상 방문할 정점이 없으면 while문 종료
      int current = Q.front(); 
      Q.pop();
      for(int i=1;i<=n;i++){
        if(G[current][i]&&!visited[current][i]){ 
          visited[G[current][i]] = 1; //현재 current와 연결된 정점을 방문.
          Q.push(G[current][i]);
        }
      }
	}
}
```

인접리스트 사용

```c++
#include<queue>
bool visited[101];
void bfs(int k){
  std::queue<int> Q;
  while(!Q.empty()){
    int current = Q.front();
    Q.pop();
    for(int i=0;i<G[current].size();i++){
      if(!visited[G[current][i]]){
        visited[G[current][i]] = 1;
        Q.push(G[current][i]);
      }
    } 
  }
}
```

