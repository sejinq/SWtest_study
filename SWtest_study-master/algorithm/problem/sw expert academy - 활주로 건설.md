# sw expert academy - 활주로 건설

경사로의 길이 X 와 절벽지대의 높이 정보가 주어질 때,

활주로를 건설할 수 있는 경우의 수를 계산하는 프로그램을 작성하라.



```java
import java.util.Scanner;
import java.io.*;
public class Solution
{
    static int[][] mapR;
    static int[][] mapC;
    static int N, X;
    static boolean check(int x){
    	if(x>N) return false;
        return true;
    }
    static boolean filght(int[] map){
    	int index=1;
        int cnt=1;
        while(index<N){
            int a = map[index]-map[index+1];
            switch(a){
                case 0:
                    cnt++; index++;
                    break;
                case 1:
                    for(int i=1;i<X;i++){
                        if(!check(index+1+i)) return false;
                    	if(map[index+1+i]!=map[index+1]) return false;  
                    } index+=X; cnt=0;
                    break;
                case -1:
                    if(cnt<X) return false;
                    index++; cnt=1;
                    break;
                default:
                    return false;
            }
        }
        return true;
    }
	public static void main(String args[]) throws IOException
	{
        Scanner sc = new Scanner(System.in);
		int T;
		T=sc.nextInt();
		for(int test_case = 1; test_case <= T; test_case++)
		{
			int answer=0;
           	N = sc.nextInt(); X = sc.nextInt();
           	mapR = new int[N+1][N+1];
            mapC = new int[N+1][N+1];
            for(int i=1;i<=N;i++){
                for(int j=1;j<=N;j++){
                    mapR[i][j] = sc.nextInt();
                    mapC[j][i] =  mapR[i][j];
                }
            }
            for(int i=1;i<=N;i++){
            	if(filght(mapR[i])) answer++;
                if(filght(mapC[i])) answer++;
           }
        	System.out.println("#"+test_case+" "+answer);
        }
	}

}
```

