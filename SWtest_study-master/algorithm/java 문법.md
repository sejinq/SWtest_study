# java 문법

import java.util.*;

import java.io.*;

## string

- indexOf : 지정한 문자가 문자열의 몇번째에 있는지 반환, 없을 시 -1

  ```java
  String str="abce";
  str.indexOf("b");	//result : 1
  ```

  ​

- length : 문자열의 길이 반환

  ```java
  String str="aaa";
  int length = str.length(); //length = 3;
  ```

  ​

- replace : 문자열에 지정한 문자 a가 있으면 새로 지정하는 b로 바꿔서 반환

  ```java
  String str= "A+B+C+D";
  String replace = str.replace("+","-");	//replace = "A-B-C-D";
  ```

  ​

- split : 지정한 문자로 문자열을 나눠 배열로 반환

  ```java
  String str = "A.B.C.D.E";
  String[] arr = str.splite(".");	//arr[0] : A, arr[1] : B.... 
  ```

  ​

- substring : 문자열의 범위에 포함되는 문자열 반환

  ```java
  String str = "ABCDEF";
  str = str.substring(0, 2); //str = "AB", 2보다 작은 범위까지
  ```

  ​

- compareTo : 두개의 String을 앞에서부터 순차적으로 비교하다 다른 부분의 char값의 차를 반환. 

  ```java
  String str1 = "A";
  String str2 = "B";
  int compareTo = str1.compareTo(str2); 
  if(compareTo>0)	//str1이 더 나중 순서(사전 순서 중)
  else if(compareTo==0)	//str1==str2
  else if(compareTo<0)	// str2가 더 나중 순서
  ```

  ​

- contains : 두개의 string을 비교해서 포함되면 true, 다르면 false

  ```java
  String origin = "ABCED";
  String temp = "AB";
  if(origin.contains(temp))	//result : true
  ```

  ​

- charAt : 지정한 index번째 문자를 반환

  ```java
  String str = "ABCDE";
  char a = str.charAt(1);	//a = 'B';
  ```

  ​

- equals : 두개의 string 값을 비교해서 같으면 true, 다르면 false 반환

  ```java
  String str1= "java";
  String str2 = "java";
  if(str1.equals(str))	//result : true
  ```



## String Tokenizer

```java
String str = "mama iii, ddddd eee";
StringTokenizer st = new StringTokenizer(str, " ");	//str을 " "으로 split
while(st.hasMoreTokens()){
    System.out.println(st.nextToken());
}
```



## List

선언

```java
public static List list = new ArrayList();
List<class> list = new ArrayList<class> (); 
```

추가

```java
list.add(index, value);
list.add(value);
```

삭제

```java
list.remove(index);
list.clear();	//전체삭제	
```

조회

```java
list.get(index);
int index = list.indexOf(value);	//해당 값의 index를 검색할 수 있음
boolean isContain = list.contains(value);	//포함관계인지 검사할 수 있음 true/false
list.size();	//list의 크기만큼 조회할 때 사용할 수 있음	
```



## Stack

선언

```java
Stack s = new Stack();
//값 입력 : s.push(value)
s.push(1);
s.push(2);
s.push(3);
//top에 있는 값을 단순검사 : s.peek()
while(!s.isEmpty()){
  	//값을 꺼낸다 : s.pop()
    System.out.println(s.pop());
}
/*전체 길이 : s.size()
  전체 삭제 : s.clear()
*/
Stack<Character> sc = new Stack<Character>();	
```



## Queue

선언 : LinkedList로 한다

```java
Queue q = new LinkedList();
//값 추가 : q.offer(value)
q.offer("1");
q.offer("2");
q.offer("3");

//단순 front의 값을 검사  :q.peek()
while(!q.isEmpty()){
  //값 꺼내기 : q.poll()
    System.out.println(q.poll());
}
```

