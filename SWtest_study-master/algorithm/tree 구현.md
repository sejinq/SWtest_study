# tree 구현

```java
import java.util.*;
import java.io.*;
 
class Node{
    String data;
    ArrayList<Integer> child ;
    public Node(String data){
        this.data = data;
        child = new ArrayList<Integer>();
    }
    public int getChild(int i){
        return child.get(i);
    }
}
class Solution{
    static String answer="";
    static Node[] node;
    static void search(Node n){
        if(n.child.size()==0){
            answer+=n.data;
            return;
        }
        search(node[n.getChild(0)]);
        answer+=n.data;
        if(n.child.size()>1){
            search(node[n.getChild(1)]);
        }
         
    }
    public static void main(String[] args)throws IOException{
        BufferedWriter bw= new BufferedWriter(new OutputStreamWriter(System.out));
        BufferedReader br= new BufferedReader(new InputStreamReader(System.in));
        for(int loop=1;loop<=10;loop++){
            int num = Integer.parseInt(br.readLine());
            node = new Node[num+1];
            while(num-->0){
                String input = br.readLine();
                StringTokenizer st = new StringTokenizer(input, " ");
                int index = Integer.parseInt(st.nextToken());
                String data = st.nextToken();    
                node[index] = new Node(data);
                while(st.hasMoreTokens()){
                    int temp = Integer.parseInt(st.nextToken());
                    node[index].child.add(temp);
                }
            
            }
            search(node[1]);
            bw.append("#"+loop+" "+answer+"\n");  answer="";
        }
        bw.flush();
        bw.close();
    }
}
```

