Follows https://github.com/TalAter/SpeechKITT/issues/25#issuecomment-307701808

To [run an HTTPS server on localhost](https://gist.github.com/dergachev/7028596):

1. Generate server.pem with `openssl req -new -x509 -keyout server.pem -out server.pem -days 365 -nodes`
2. Create a python script *simple-https-server.py* with code:
 ```
import BaseHTTPServer, SimpleHTTPServer
import ssl

httpd = BaseHTTPServer.HTTPServer(('localhost', 4443), SimpleHTTPServer.SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket (httpd.socket, certfile='./server.pem', server_side=True)
httpd.serve_forever()
```
3.  Run `python simple-https-server.py` then in your browser, visit https://localhost:4443
