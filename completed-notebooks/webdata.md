Session X: Working with webdata
====

This is a crash course adapted from @DrChunk's [Coursera Python course](https://www.coursera.org/learn/python-network-data/home/welcome). Free Python textbook also available: https://goo.gl/khBOeX (the chapters relating to this crash course are Chapter 11-13).

We will cover the three set of slides that can also be found:

 - [Regex](https://docs.google.com/presentation/d/1x7AyMWJqL6w15ig-xZ6vTDsnaqxkIcumLueCVs0RpCI/edit#slide=id.p49)
 - [Network Programming](https://docs.google.com/presentation/d/1MxNWMKceFNqwhUGabIfdmpHCQcowmeMgpMNuOZC8fdc/edit#slide=id.p64)
 - [Web Services](https://docs.google.com/presentation/d/1NsmEzcCMYuBrfm0lRrUVAoI2Rxou3xn9wpDwnfCAH2k/edit#slide=id.p61)


This will be a prelude to more detailed lessons on XML, JSON, REST, Scrapping the web, ...





How do computer communicate?
====

Computer communicate through applications and protocols that governs/controls the communication. 

**What is socket programming?**

```
import socket

mysock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
mysock.connect(('www.py4inf.com', 80))
mysock.send('GET http://www.py4inf.com/code/romeo.txt HTTP/1.0\n\n')

while True:
    data = mysock.recv(512)
    if ( len(data) < 1 ) :
        break
    print data;

mysock.close()
```



**Before we continue, try this code in python**

```
import antigravity
```


**How to download and read a file**

```
#!/usr/bin/env python3 -*- coding: utf-8 -*-

import re
import urllib.request
link = 'http://pr4e.dr-chuck.com/tsugi/mod/python-data/data/regex_sum_183416.txt'
response = urllib.request.urlopen(link)
text = response.read().decode()
print(text)
```


Regex: The programming language inside another programming language.
====

**Find all digits and sum them up!**

```
#!/usr/bin/env python3 -*- coding: utf-8 -*-

import re
import urllib.request
link = 'http://pr4e.dr-chuck.com/tsugi/mod/python-data/data/regex_sum_183416.txt'
response = urllib.request.urlopen(link)
text = response.read().decode()

print (sum(map(int, re.findall('[0-9]+', text))))
```


**Let's read a webpage and extract things we want**

Download a page, read the 17th link and go to that link and download the page again, read the 17th link, ... (do it 7 times)

```
#!/usr/bin/env python3 -*- coding: utf-8 -*-

import urllib.request
from bs4 import BeautifulSoup

link = 'http://pr4e.dr-chuck.com/tsugi/mod/python-data/data/known_by_Rodrigo.html'

for _ in range(7):
	response = urllib.request.urlopen(link)
	html = response.read()
	bsoup = BeautifulSoup(html)
	eighteenth = bsoup.find_all('a')[17]
	link = eighteenth['href']

print(eighteenth.text)
```

XML: eXentensible Markup Language
===

**Download the XML file, find all the numbers embedded within <count>...</count> and sum them up.**

```
#!/usr/bin/env python3 -*- coding: utf-8 -*-
import urllib.request
import xml.etree.ElementTree as ET

link = 'http://pr4e.dr-chuck.com/tsugi/mod/python-data/data/comments_183418.xml'

response = urllib.request.urlopen(link)
xmldata = response.read()
tree = ET.fromstring(xmldata)
counts = tree.findall('.//count')
sum_counts = sum(int(c.text) for c in counts)
print (sum_counts)
```

JSON: 
====

**Download the JSON file, find the `count` key and sum its value up**

```
#!/usr/bin/env python3 -*- coding: utf-8 -*-
import urllib.request
import json

link = 'http://pr4e.dr-chuck.com/tsugi/mod/python-data/data/comments_183422.json'

response = urllib.request.urlopen(link)
jsondata = response.read()
j = json.loads(jsondata.decode())
print (sum(i['count'] for i in j['comments']))
```

API:
====

Using the Google Geocode API, find the ID of a place `Masdar Institute`

```
#!/usr/bin/env python3 -*- coding: utf-8 -*-

import urllib.parse
import urllib.request
import json

serviceurl = 'http://maps.googleapis.com/maps/api/geocode/json?'
address = 'Masdar Institute'
link = serviceurl + urllib.parse.urlencode({'sensor':'false', 'address': address})
response = urllib.request.urlopen(link)
jsondata = response.read()
j = json.loads(jsondata.decode())

print(j['results'][0]['place_id'])
```
