# String Match

**Input** ? : 아무 알파벳이나 1글자  \*: 그 뒤 글자가 최소 0개 이상의 반복

>다음과 같은 패턴 매칭 룰이 있다. 패턴과 문자열이 주어질때, 주어진 문자열 전체가 주어진 패턴으로 매칭되는지 아닌지를 판단하는 코드를 작성하시오. (주의. 정규표현식과는 세부 규칙이 다르다.)
>
>패턴은 영어 알파벳 소문자, 특수문자로 이루어져 있고, 문자열은 영어 알파벳 소문자로 이루어져 있다. 입력으로 주어지는 패턴의 길이는 1 <= length <= 1,000 이다. 입력으로 주어지는 문자열의 길이는 1 <= length <= 1,000 이다.
>
>특수문자는 ?, * 중에 하나이며, 의미는 아래와 같다. 알파벳 소문자는, 그 글자 그대로를 의미한다. 글자가 일치하면 매칭된다. ?은 아무 알파벳이나 1글자를 의미한다. *은 그 뒤의 글자가 최소 0개 이상의 반복되는 것을 의미한다. * 은 혼자 입력으로 주어지지 않는다. *a 이면 연속된 a가 0개 이상을 의미한다. 빈 문자열 "" 또는 "a", "aa", "aaa" 등이 해당된다. *? 는 ?(아무 글자)가 0개 이상을 의미하므로, 0개 이상의 아무 글자를 의미한다. "abcdefg" 등의 연속된 아무 글자가 매칭된다.
>
>입력 형식
>
>첫 줄에는 TC의 개수가 입력된다. 각 TC 횟수만큼, 각 줄에, 패턴 문자열과, 검사할 문자열 2개를 입력받는다.
>
>출력 형식
>
>각 줄에, O 또는 X 를 대문자로 출력한다. 
>
>␣  : 공백 ↵ : 줄바꿈
>
>입력 
>
>9
>
>aaa aaa
>
>a?a aaa
>
>ab aa
>
>*ab aaaab
>
>a*b*c abc
>
>a*b*c a
>
>b*ccd bd
>
>*? abcdefg
>
>a*?b alineb9
>
>출력 
>
>O↵
>
>O↵
>
>X↵
>
>O↵
>
>O↵
>
>O↵
>
>X↵
>
>O↵
>
>O↵




```java
import java.io.*;
import java.util.*;
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class Solution {
    public static void pmatch(String newstr, String output){
        /*newstr문자열에 *부분 먼저 치환
        *a : a문자를 0번 이상 반복
        = 정규식 표현 : a*(*앞의 문자를 0번 이상 반복) */
        int check=-2;
        while(true){
          // *부분의 index를 찾는다. 치환부의 *가 검색에 걸리지 않도록 check+2의 인덱스를 검색 시작위치로 지정해준다.
	  //*a가 a*로 바뀌니까 +2를 해주어야함
            check = newstr.indexOf("*", check+2);
          
            //*가 더이상 존재하지 않거나 마지막 부분에 위치할 시 무한루프 종료
            if(check<0||check==newstr.length()-1) break; 
          
            //*의 다음 1개의 문자를 추출.(반복할 문자) 
            String sub = newstr.substring(check, check+2);  
            char temp = sub.charAt(1); 
          
            //문자열을 정규식 표현법으로 치환
            newstr = newstr.replace(sub, temp+"*"); 
        }
      
      /*newstr문자열의 ?부분 치환
        ?를 먼저 치환해버리면 *?부분을 예외로 치환해야되기때문에 후순위로 치환한다.
        ? : 아무 알파벳이나 1개
        = 정규식 표현 : [A-Za-z](대문자 A-Z, 소문자 a-z까지 아무 문자나 1개)*/
        newstr = newstr.replace("?", "[A-Za-z]");
      //정규식 만들기 pattern 클래스를 이용해서 ^(정규식의 시작) $(정규식의 끝)을 더해 정규식을 만들어준다.
        Pattern pattern = Pattern.compile("^"+newstr+"$");
      //만들어진 정규식에 검사할 문자열 output이 부합하는지 검사
        Matcher matcher = pattern.matcher(output);
      
        if (matcher.matches()) System.out.println("O");
        else System.out.println("X");
    }
  
    public static void main(String args[]) throws IOException {
		Scanner scn = new Scanner(System.in);
        int tc = scn.nextInt(); scn.nextLine();
        for(int loop=1;loop<=tc;loop++){
        	String patternstr = scn.next(); 
            String matchstr = scn.next();
            pmatch(patternstr, matchstr);    
    }
 }}
```



java string http://itpangpang.xyz/275
<br> java 정규식 http://diyall.tistory.com/768


