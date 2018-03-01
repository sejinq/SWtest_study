# Array 1

## View

- input 

  가로 길이를 입력 받음

  가로 길이 만큼의 0-1000이하의 수가 들어온다.



- output	

  좌, 우로 2칸씩 겹치지 않는 블록의 수 

>풀이방법
>
>좌, 우의 높이 값을 뺐을 때, 모두 양수이면 view가 확보되는 블록



```java
import java.util.Scanner;
import java.util.Arrays;

class View {
  public static void main(String[] args) {
    Scanner scn = new Scanner(System.in);
      for(int loop=1;loop<=10;loop++){ 
        int len = scn.nextInt();
        int[] building = new int[len];
        for(int i=0;i<len;i++){
            building[i] = scn.nextInt();
        }
        int viewResult=0;
        int[] temp = new int[4];
        for(int i=2;i<len-2;i++){
            temp[0] = building[i] - building[i-1];
            temp[1] = building[i] - building[i-2];
            temp[2] = building[i] - building[i+1];
            temp[3] = building[i] - building[i+2];

            if(temp[0]<=0||temp[1]<=0||temp[2]<=0||temp[3]<=0){
                continue;
            }
          	Arrays.sort(temp);
            viewResult+= temp[0];
        }
        System.out.println("#"+loop+" "+viewResult);
        
      }
      building = null;
 }  
}
```



