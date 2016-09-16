
Python Challenge
=================


No.1
----
http://www.pythonchallenge.com/pc/def/map.html

凯撒密码， K->M, O->Q, E->G, 位移了2
因此对标题 map 进行位移2操作，得到 ocr


No.2
----
http://www.pythonchallenge.com/pc/def/ocr.html

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
http://www.pythonchallenge.com/pc/def/equality.html

查看页面源代码，找到注释，保存为 3.txt
``` python
import re
f = open('3.txt','r')
hints = f.read()
f.close()
x = re.findall('r[a-z][A-Z]{3}[a-z][A-Z]{3}[a-z]',hints)
print ''.join([i[4] for i in x]) # linkedlist
```


No.4
----
http://www.pythonchallenge.com/pc/def/linkedlist.html

查看源代码，提示follow the chain, 点击图片进入循环
``` python
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
http://www.pythonchallenge.com/pc/def/peak.html

查看源代码，提示 peak hell 与 pickle 发音类似, 下载 banner.p
``` python
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
http://www.pythonchallenge.com/pc/def/channel.html

拉链为 zip, 查看源代码，提示 html <- zip, 将地址上html 改为zip，下载
channel.zip, 查看readme.txt, start from 90052, 打开90052, 与之前linkedlist类似。
``` python
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
``` python
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
http://www.pythonchallenge.com/pc/def/oxygen.html

图片 oxygen.png 中间存在灰度图片，使用PIL提取灰度图的灰度值，作为ascii码
``` python
from PIL import Image
fig = Image.open('oxygen.png')
col = [ fig.getpixel((3,y)) for y in range(fig.size[1])]
ns = [i for i, p in enumerate(col) if p[0]==p[1]==p[2]] # [43, 44, ..., 51]
n = ns[3]
row = [ fig.getpixel((x,n)) for x in range(fig.size[0])]
info = [r for r,g,b,a in row if r==g==b]
"".join(map(chr, info[::7]))
# come up with  [105, 110, 116, 101, 103, 114, 105, 116, 121]
next =  [105, 110, 116, 101, 103, 114, 105, 116, 121]
"".join(map(chr, next)) # integrity
```


No.8
----
http://www.pythonchallenge.com/pc/def/integrity.html

网页源代码中写出 username, password
两个字符串经过bz2压缩，因此需要解压才可。
```python
import bz2
un = 'BZh91AY&SYA\xaf\x82\r\x00\x00\x01\x01\x80\x02\xc0\x02\x00 \x00!\x9ah3M\x07<]\xc9\x14\xe1BA\x06\xbe\x084'
pw = 'BZh91AY&SY\x94$|\x0e\x00\x00\x00\x81\x00\x03$ \x00!\x9ah3M\x13<]\xc9\x14\xe1BBP\x91\xf08'

print bz2.decompress(un) # huge
print bz2.decompress(pw) # file
```


No.9
-----
http://www.pythonchallenge.com/pc/return/good.html

不知道什么意思。找到的答案为
``` python
first = [146,399,163,403,170,393,169,391,166,386,170,381,170,371,170,355,169,346,167,335,170,329,170,320,170,
310,171,301,173,290,178,289,182,287,188,286,190,286,192,291,194,296,195,305,194,307,191,312,190,316,
190,321,192,331,193,338,196,341,197,346,199,352,198,360,197,366,197,373,196,380,197,383,196,387,192,
389,191,392,190,396,189,400,194,401,201,402,208,403,213,402,216,401,219,397,219,393,216,390,215,385,
215,379,213,373,213,365,212,360,210,353,210,347,212,338,213,329,214,319,215,311,215,306,216,296,218,
290,221,283,225,282,233,284,238,287,243,290,250,291,255,294,261,293,265,291,271,291,273,289,278,287,
279,285,281,280,284,278,284,276,287,277,289,283,291,286,294,291,296,295,299,300,301,304,304,320,305,
327,306,332,307,341,306,349,303,354,301,364,301,371,297,375,292,384,291,386,302,393,324,391,333,387,
328,375,329,367,329,353,330,341,331,328,336,319,338,310,341,304,341,285,341,278,343,269,344,262,346,
259,346,251,349,259,349,264,349,273,349,280,349,288,349,295,349,298,354,293,356,286,354,279,352,268,
352,257,351,249,350,234,351,211,352,197,354,185,353,171,351,154,348,147,342,137,339,132,330,122,327,
120,314,116,304,117,293,118,284,118,281,122,275,128,265,129,257,131,244,133,239,134,228,136,221,137,
214,138,209,135,201,132,192,130,184,131,175,129,170,131,159,134,157,134,160,130,170,125,176,114,176,
102,173,103,172,108,171,111,163,115,156,116,149,117,142,116,136,115,129,115,124,115,120,115,115,117,
113,120,109,122,102,122,100,121,95,121,89,115,87,110,82,109,84,118,89,123,93,129,100,130,108,132,110,
133,110,136,107,138,105,140,95,138,86,141,79,149,77,155,81,162,90,165,97,167,99,171,109,171,107,161,
111,156,113,170,115,185,118,208,117,223,121,239,128,251,133,259,136,266,139,276,143,290,148,310,151,
332,155,348,156,353,153,366,149,379,147,394,146,399]

second = [156,141,165,135,169,131,176,130,187,134,191,140,191,146,186,150,179,155,175,157,168,157,163,157,159,
157,158,164,159,175,159,181,157,191,154,197,153,205,153,210,152,212,147,215,146,218,143,220,132,220,
125,217,119,209,116,196,115,185,114,172,114,167,112,161,109,165,107,170,99,171,97,167,89,164,81,162,
77,155,81,148,87,140,96,138,105,141,110,136,111,126,113,129,118,117,128,114,137,115,146,114,155,115,
158,121,157,128,156,134,157,136,156,136]

from PIL import Image, ImageDraw
img = Image.new("RGB", (640,480))
draw = ImageDraw.Draw(img)
draw.line(first)
draw.line(second)
img.save('new.jpg')
```
得到一头公牛的图片，bull


No.10
-----
http://www.pythonchallenge.com/pc/return/bull.html

点击图片，可以看到数列 a = [1, 11, 21, 1211, 111221,
求 len(a[30])
规律就是读出数字，1个1-> 11, 两个1 -> 21, ...

``` python
import re

pat = re.compile(r'1+|2+|3+|4+|5+|6+|7+|8+|9+')

def say(numstr):
    curr = pat.findall(numstr)
    next = "".join([str(len(s))+s[0] for s in curr])
    return next
n = 0
a = '1'
while n<30:
    a = say(a)
    n += 1
print len(a) # 5808
```


No.11
------
http://www.pythonchallenge.com/pc/return/5808.html

提示是奇偶。对图片的奇偶进行提取
``` python
from PIL import Image

img =  Image.open('cave.jpg')
width, length = img.size

subimgs = [Image.new("RGB",width//2,length//2) for i in range(2)]

for x in range(width):
    i = x % 2
    sub = subimgs[i]
    for y in range(length):
        sub.putpixel((x//2, y//2),img.getpixel((x,y)))

subimg[0].save('even.jpg')
subimg[1].save('odd.jpg') # evil
```


No.12
-----
http://www.pythonchallenge.com/pc/return/evil.html

图片地址为 evil1.jpg, 改为 evil2.jpg: not jpg -gfx
evil3.jpg: no more evils
evil2.gfx: 得到这个文件

``` python
import StringIO
from PIL import Image

with open('evil2.gfx','r') as f:
    data = f.read()
for i in range(5):
    p = data[i::5]
    f = open('No.12-%d.jpg' %i, 'wb')
    f.write(p)
    f.close() # check jpgs, disproportional
```


No.13
-----
http://www.pythonchallenge.com/pc/return/disproportional.html

为一个XML-RPC server, 因此

```python
import xmlrpclib
url = "http://www.pythonchallenge.com/pc/phonebook.php"
phonebook = xmlrpclib.Server(url)
print phonebook.system.listMethods()
print phonebook.system.methodHelp("phone")
print phonebook.phone("Bert") # 555-ITALY
```

## No.14

点开图片发现图片的大小是10000*1, 螺旋和提示`100*100=(100+99+99+98)+(...)`
```python
from PIL import Image

width = 100
wire = Image.open("wire.png")
new_img = Image.new(wire.mode, (width, width), color=0)

def get_xy(width=width):
    x, y = 0, 0
    w = width
    while True:
        # print(x, y, "---->")
        for j in range(w):
            yield x, y
            x += 1
        x -= 1
        # print("---->|", x, y)
        y += 1
        for j  in range(w-1):
            yield x, y
            y += 1
        y -= 1
        # print("<----", x,y)
        x -= 1
        for j in range(w-1):
            yield x, y
            x -= 1
        x += 1
        # print("|<----", x,y)
        y -= 1
        for j in range(w-2):
            yield x, y
            y -= 1
        y += 1
        x += 1
        w -= 2

xy  = get_xy(width=width)

for i in range(width*width):
    x, y  = xy.next()
    new_img.putpixel((x,y), wire.getpixel((i, 0)))

new_img.show() # cat -> uzi
```

## No.15
图片中为日历，并且右下角2月有29天，因此为闰年，注释中提到是第二年轻的
```python
from calendar import isleap, weekday
for year in range(1006, 2000, 10):
    if isleap(year) and weekday(year, 1, 26) == 0:
        print year
# 1176, 1356, 1576, 1756, 1976
```
1756.1.27 莫扎特出生 mozart

## No.16
按照图的意思应该是根据粉色的标记进行重排
```python
from PIL import Image
PINK = 195
mess = Image.open("mozart.gif")
new_img = Image.new(mess.mode, mess.size)
width = mess.size[0]
data = list(mess.getdata())
new_data = list(data)
for head in range(0, len(data), width):
    pink = data.index(PINK, head)
    new_data[head:head+width] = data[pink:head+width]+data[head:pink]
new_img.putdata(new_data)
new_img.show() # romance
```
## No.17
