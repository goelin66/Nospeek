現在外面好多人在說 #Python

聽說自己爬文學習也能, 想說從爬蟲開始練習

沒想到在安裝就碰到問題了...

## 很重要, 如果pip無法安裝請直接使用 Anaconda Navigator 的軟體

## 下面都可以不用理了, 因為根本沒用阿!

等我有解在寫

要在pthyon安裝的地方打開cmd後執行python3皆著...輸入

```python
pip install lxml
```
![](https://raw.githubusercontent.com/goelin66/Nospeek/74b9e39e39657a9efdea6988a541ee23b59fcc82/pic/Loss.PNG)

TNND 居然說我沒安裝 Visual C++

好吧我真的沒安裝

上了[wiki的Python](https://wiki.python.org/moin/WindowsCompilers)看一下我需要安裝啥版本的

安裝完成後..

還是給我跳一樣的情況我傻眼了....

接著爬文...

很好我找到答案了, 但我擔心這網站我忘了所以自己再打一份留著

[Python 3.6 模块安装“error: Microsoft Visual C++ 14.0 is required...”问题解决](https://blog.csdn.net/u011389474/article/details/60764926)

照著這網站的做..

直接走最後套路

到[Python Extension Packages(https://www.lfd.uci.edu/~gohlke/pythonlibs/)找到你要的

下載完丟到你Python的安裝Path

一路點安裝沒看仔細裝在那?

```
C:\Users\Admin\AppData\Local\Programs\Python\Python37-32
```

大概就在這邊啦~

丟進去後就cmd一路cd到這個Path下吧

不會?

開始打cmd

開始跟著我打 

#( 使用者名稱自己換一下喔~~~ )

```cmd
cd AppData
cd Local
cd Programs
cd Python
cd Python37-32
cd lxml-master
pip install -r requirements.txt
python setup.py install
```
