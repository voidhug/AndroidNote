网络
===

```shell
telnet tiem-A.timefreq.bldrdoc.gov 13   

浏览器访问某个页面
telnet java.sun.com 80
GET / HTTP/1.0
```


```java
public class SocketTest {
    public static void main(String[] args) {
        try {
            Socket s = new Socket("time-A.timefreq.bldrdoc.gov", 13);
            try {
                InputStream inputStream = s.getInputStream();
                Scanner in = new Scanner(inputStream);
                while (in.hasNextLine()) {
                    String line = in.nextLine();
                    System.out.println(line);
                }
                inputStream.close();
            } finally {
                s.close();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```



