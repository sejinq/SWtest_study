# Array 1

## Flatten

정해진 횟수 내에 덤프(최대 높이와 최저 높이간의 차이를 줄이는)하는 문제

- input

  덤프 횟수가 주어진다.

  100개의 입력값이 주어지고 값의 범위는 1-100이다.

- output

  덤프 횟수가 끝났을 때 최고점-최저점의 높이 차를 반환한다.

  만약 덤프 횟수 내에 평탄화가 완료(0-1)되면 그 때의 값을 반환한다.

>풀이방법
>
>한번의 덤프가 끝날 시에 sort를 통해 최고점과 최저점을 구하여
>
>덤프 후 다시 sort. 
>
>시간은 많이 걸리나 가장 확실한 방법이다.



```
import java.util.*;
```

<c++>

```c++
#include<iostream>
#include<algorithm>
using namespace std;

int main(){
  for(int loop=1;loop<=10;loop++){
    int answer=0;
    int dump=0;
    int arr[100]={0, };
    cin>>dump;
    for(int i=0;i<100;i++){
        cin>>arr[i];
    }
    while(dump--){
    	sort(arr, arr+100);
      	if(arr[99]-arr[0]<=1) break;
        arr[0]++; arr[99]--;
    }
    sort(arr, arr+100);
    answer = arr[99]-arr[0];
    
    cout<<"#"<<loop<<" "<<answer<<endl;
  }
	return 0;
}
```

