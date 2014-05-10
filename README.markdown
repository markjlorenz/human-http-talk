# Human HTTP Server

1) start `nc -l`
2) `nc` to `nc -l` for sending text
3) `nc -k -l`
4) hit the `nc -k -l` from the browser
  ```
  GET /hello-world HTTP/1.1
  Host: localhost:3000
  Connection: keep-alive
  Cache-Control: max-age=0
  Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
  User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/34.0.1847.116 Safari/537.36
  Accept-Encoding: gzip,deflate,sdch
  Accept-Language: en-US,en;q=0.8,gl;q=0.6
  ```

  ```
  HTTP/1.1 200 OK
  Last-Modified: Sun, 13 Apr 2014 01:40:40 GMT
  Content-Type: text/html
  Content-Length: 5906
  Server: WEBrick/1.3.1 (Ruby/2.0.0/2013-06-27)
  Date: Wed, 30 Apr 2014 03:07:50 GMT
  Connection: Keep-Alive
  ```

5) respond from `nc -k -l`
  ```
  HTTP/1.1 200 OK
  ```

6) respond with text from `nc -k -l`
  ```
  HTTP/1.1 200 OK
  Content-Type: text/plain

  hello world
  ```

7) respond with HTML from `nc -k -l`
  ```
  HTTP/1.1 200 OK
  Content-Type: text/html

  <h1>hello world</h1>
  ```

8) respond with HTML including JS from `nc -k -l`
  ```
  HTTP/1.1 200 OK
  Content-Type: text/html

  <script src="/script.js"></script>
  ```

  ```
  HTTP/1.1 200 OK
  Content-Type: application/javascript

  alert("hello world");
  ```

9) go get jQuery and manipulate the DOM
  ```
  HTTP/1.1 200 OK
  Content-Type: text/html

  <script src="//code.jquery.com/jquery-latest.js"></script>
  <script>jQuery(function($){ $('body').append('<h1>hello world</h1>'); });</script>
  ```

10) go get jQuery and get JSON
  ```
  HTTP/1.1 200 OK
  Content-Type: text/html

  <script src="//code.jquery.com/jquery-latest.js"></script>
  <script src="/hello-world.js">
  </script>
  ```

  ```
  HTTP/1.1 200 OK
  Content-Type: application/javascript

  jQuery(function($){
    json = $.getJSON('/hello-world.json');
    json.done(function(data){
      alert(data.hello);
    });
  });
  ```

  ```
  HTTP/1.1 200 OK
  Content-Type application/json

  {"hello": "world"}
  ```

11) send a gzip'd file
  ```
  HTTP/1.1 200 OK
  Content-Type: text/plain
  Content-Encoding: gzip

  ^_<8b>^H^@Ý^LcS^@^C+,M-.ÉÌÏ+¶ç^B^@¶ÿ<9b>i^K^@^@^@
  ```
