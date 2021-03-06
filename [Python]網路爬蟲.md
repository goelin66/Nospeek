網路上查詢很多種做法

這邊是記錄我自己一步一步網路查詢製作的教學

因為不一定會成功,

但我想把跌跌撞撞的路途記錄下來,

避免下次再犯或者以後回頭時可以了解當初犯錯的原因

希望這樣能幫助到後面也有人想完這東西時

可以少撞一些牆或者了解要怎麼摧毀這牆...

那麼首先是我第一個碰到的問題

安裝完後要幹嘛?

在安裝完的路徑內可以看到 python.exe 的應用程式

啟用會發現是透過cmd來執行

不過你實際打cmd卻又不能使用喔

另外 powershell 目前測試好像不支援
( 因為我不確定所以用我測試好像不支援 )

而我覺得有個軟體不錯用

Cmder 喜歡自己網路上查一下吧

這程式的畫面我覺得比 cmd 漂亮多了

但切記要安裝在 python.exe 這程式的相同資料夾內喔

接著就開始玩吧

對了, 以下的練習都是在Cmder下運行

我一個程式結束就請輸入enter讓他載入

那開使江程式打開並輸入

```python
python3
```

這指令會幫你去將你安裝路境內的 python.exe 運行起來

那...因為之前測試時我已經安裝了很多鬼軟體

先講基本要安裝的

BeautifulSoup4

那安裝方法就是輸入

```python
pip install BeautifulSoup4
```

實際照片跟在那邊輸入我晚點再補上吧

其他需要的我也晚點再補

接著完成後

我們要來用 BeautifulSoup4 來抓取資料

因為 BeautifulSoup4 已經移直到 bs4 上

那什麼是 bs4?

我有空再去查

```python
from bs4 import BeautifulSoup
```

接著將 html_doc 設定起來

```python
html_doc = """
```

這邊打玩其實你會發現 Cmder 會從 【 >>> 】 變成 【 。。。 】

那就是要開始將網頁的架構邊寫完成擺放到 html_doc 內

那怎擺放? 我有空在細查了...

再把架構慢慢邊寫起來吧

```python
<html><head><title>The Dormouse's story</title></head>
```

這邊以下的語法我都是先借用別人的

```python
<body>
```

```python
<p class="title"><b>The Dormouse's story</b></p>
```

```python
<p class="story">Once upon a time there were three little sisters; and their names were
```

```python
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
```

```python
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
```

```python
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
```

```python
and they lived at the bottom of a well.</p>
```

```python
<p class="story">...</p>
```

```python
"""
```

到這邊就完成了把 html_doc 套用的網頁架構設定好了

接著使用 BeautifulSoup4 的功能了

將 html_doc 轉格是餵到 BeautifulSoup4 內

```python
soup = BeautifulSoup(html_doc, 'html.parser')
```

接著我們能測試有沒有餵成功

```python
print(soup.prettify())
```

如果有會有下面的資訊

![soup](https://github.com/goelin66/Nospeek/blob/master/pic/intosoup.PNG?raw=true)

嗯....

初步知到要怎查資料了

但還不是爬蟲阿!!!!

所以我又找了一下去 jupyter

安裝 Anconda...

反正測試看看了

失敗在重灌電腦了~~~

安裝完成後他會要你開啟程式

程式能幫你跑那些python的程式碼

但安裝卻要用他的 Anconda Promt 去安裝

好吧

因為我測試到要透過 selenium 去開網頁時卡關了

![111](https://github.com/goelin66/Nospeek/blob/master/pic/111.PNG?raw=true)

乾! 才發現安裝跟編寫要用不同的東西

好吧接著看...

透過 selenium 去爬網頁上的資訊

那要讓 selenium 能開啟你的瀏覽器

就必需安裝 [瀏覽器的Driver](http://chromedriver.chromium.org/downloads)

這邊教學就用chrome

其它有興趣在自己找吧

不然就等我開心在補

```python
from selenium import webdriver
from bs4 import BeautifulSoup

url = 'https://www.google.com.tw/search?q=python%E7%88%AC%E8%9F%B2&oq=python%E7%88%AC%E8%9F%B2&aqs=chrome..69i57j69i59l2j69i61l2j0.2543j0j7&sourceid=chrome&ie=UTF-8' # 把網址輸入


chromedriver = "E:\Download\learning\WebDriver\chromedriver" # 輸入Driver擺放的位址
driver = webdriver.Chrome(chromedriver) # 載入Driver

driver.get(url)  # 把網址交給瀏覽器
pageSource = driver.page_source  # 取得網頁原始碼
soup = BeautifulSoup(pageSource, 'lxml')  # 解析器接手
result = soup.select('#resultStats')[0].get_text()
print('python爬蟲', result)

# python爬蟲 約有 297,000 項結果 (搜尋時間：0.34 秒)
```

這樣初步要爬資料的樣子終於有出來了...


2018/08/04
今天想說測試一下爬蟲的功用

如果不透過上面方是用瀏覽器去查也可以, 

不過要知道開啟的網頁是哪種格式, json? html?

好吧我也都看別人文章寫得去學著寫,

那今天的內容是如何透過爬蟲來找便宜的商品！

好比我想在PChome上找便宜的設備 ( 有點雞肋 )

首先要先點開F12接著開始查詢pchome

透過收尋商品能找 SSD

![24Hpchome](https://github.com/goelin66/Nospeek/blob/master/pic/24Hpchome.PNG)

就能看到他是用 request 的指令去查詢

```python
import requests # 導入requests的物件, 每次使用都要導入一次的樣子?
from bs4 import BeautifulSoup # 因為BeautifulSoup是bs4眾多物件內的其中一個, 透過 from ... import 來選定需要的元件導入
import json # 因為這次查詢的 Pchome24H 是 json 格式

url = "https://ecshweb.pchome.com.tw/search/v3.3/all/results?q=SSD&page=1&sort=rnk/dc" # 這邊查詢SSD的第一頁
res = requests.get(url)
data = json.loads(res.text)
names=[]
prices=[]
prices1=[]
urls=[]
mainurl = 'http:/24h.pchom.com.tw/prod'
for product in data['prods'] :
    names.append(product['name'])
    price1 = product['price']
    price2 = price1 < 1000
    prices.append(price2)
    prices1.append(product['price'])
    url1=mainurl+product['Id']
    urls.append(url1)

num = len(data['prods'])-1
print(num)

print()

#print(names[num])
#print(product['price'])
#print('價格<1000 :', prices[num])
#print(urls[num])

for ii in range(num, -1, -1):
    pricess = prices[ii]
    #print(pricess)
    if pricess == True:
        i = ii
        print(names[i])
        print(prices1[i])
        print('價格<1000 :', prices[i])
        print(urls[i])
        #print(i)
```

這次參考別人家的寫法, 在改邊的。

雖然沒啥屁用, 但好玩就好啦~

最終目標是要能把MM的照片拉出來！


參考資料 : 
https://www.qa-knowhow.com/?p=3175
https://cuiqingcai.com/1319.html
http://beautifulsoup.readthedocs.io/zh_CN/latest/#id12
https://morvanzhou.github.io/tutorials/python-basic/basic/

2018/08/04
http://ivanjo39191.pixnet.net/blog/post/70548675-python-%E7%88%AC%E8%9F%B2%E7%B7%B4%E7%BF%92%E7%B4%80%E9%8C%842%28%E4%B8%80%29

同事友情給的資料
https://medium.com/pyladies-taiwan/從dcard網站看爬蟲入門-65105f0ddac
https://cuiqingcai.com/3179.html

說實話, 有網路真好...
