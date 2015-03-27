Python Challenge
=================

No.1
----
http://www.pythonchallenge.com/pcc/def/map.html
凯撒密码， K->M, O->Q, E->G, 位移了2
因此对标题 map 进行位移2操作，得到 ocr

No.2
----
http://www.pythonchallenge.com/pcc/def/ocr.html
查看页面源代码，找到注释，保存为 2.txt
``` python
f = open('2.txt','r')
hints = f.read()
f.close()
d = {}
for c in hints:
    d.setdefault(c,0)
    d[c] += 1
print d # equality
```

No.3
----
http://www.pythonchallenge.com/pcc/def/equality.html
查看页面源代码，找到注释，保存为 3.txt
```
import re
f = open('3.txt','r')
hints = f.read()
f.close()
x = re.findall('r[a-z][A-Z]{3}[a-z][A-Z]{3}[a-z]',hints)
print ''.join([i[4] for i in x]) # linkedlist
```

No.4
----
http://www.pythonchallenge.com/pcc/def/linkedlist.html
查看源代码，提示follow the chain, 点击图片进入循环
```
import requests
import re
url0 = 'http://www.pythonchallenge.com/pc/def/linkedlist.php?nothing='
n = 12345
while n:
    a = requests.get(url0+str(n))
    n = int(re.findall(r'\d+', a.text)[0])
    print n
```
中间出错几次，按照提示重新确定n，继续循环， 最后得到 peak.html

No.5
-----
http://www.pythonchallenge.com/pcc/def/peak.html
查看源代码，提示 peak hell 与 pickle 发音类似, 下载 banner.p
```
import pickle
with open('banner.p', 'r') as f:
    hints = pickle.load(f)
for l in hints:
    line = ''
    for j in l:
        line += j[0]*j[1]
    print line
```
最后出现的字符串图片为 channel

No.6
-----
http://www.pythonchallenge.com/pcc/def/channel.html
拉链为 zip, 查看源代码，提示 html <- zip, 将地址上html 改为zip，下载
channel.zip, 查看readme.txt, start from 90052, 打开90052, 与之前linkedlist类似。
```
import re
import zipfile
channels = zipfile.ZipFile('channel.zip', 'r')
n = '90052'
while n:
    lines = channel.read(str(n)+'.txt')
    n = re.findall(r'\d+',lines)[0]
    print n
```
到达 n=46145 停止， 其内容为 "Collect the comments"
因此改变循环体
```
comments = []
n = '90052'
while n:
    lines = channel.read(str(n)+'.txt')
    comments.append(channel.getinfo(str(n)+'.txt').comment)
    n = re.findall(r'\d+', lines)[0]
    print n
print "".join(comment)
```
得到的为 hockey, 由 oxygen 构成。

No.7
----
http://www.pythonchallenge.com/pcc/def/oxygen.html
