做愈久接觸愈多後發現許多問題

從RJ-45轉到Fiber?

從簡單的CAT的線換到光纖線...

這次就以光纖為主題吧。

光纖...

是用一種玻璃或塑膠製成的纖維，透過光在這些纖維中反射~~~ 這些話在[維基百科](https://zh.wikipedia.org/wiki/%E5%85%89%E5%B0%8E%E7%BA%96%E7%B6%AD)都有。

那這些訊息不是我想介紹的,

因為我碰到的是

  [1. 光纖線要怎選?](https://github.com/goelin66/Nospeek/new/master#1-%E5%85%89%E7%BA%96%E7%B7%9A%E8%A6%81%E6%80%8E%E9%81%B8)

  [2. 光模塊要怎選用?](https://github.com/goelin66/Nospeek/new/master#2-%E5%85%89%E6%A8%A1%E5%A1%8A%E8%A6%81%E6%80%8E%E9%81%B8%E7%94%A8)

  [3. 100M是包含10/100內還是100/1000內?](https://github.com/goelin66/Nospeek/new/master#3-100m%E6%98%AF%E5%8C%85%E5%90%AB10100%E5%85%A7%E9%82%84%E6%98%AF1001000%E5%85%A7)
  
  [4. 總結](https://github.com/goelin66/Nospeek/new/master#3-100m%E6%98%AF%E5%8C%85%E5%90%AB10100%E5%85%A7%E9%82%84%E6%98%AF1001000%E5%85%A7)

基於一直被問又答不出來才決定去爬文。

# 1. 光纖線要怎選? 

在此以我常用到的兩種來做介紹

**單模光纖 vs 多模光纖**

單模光纖 (Single Mode)

![單模光纖](http://images.100y.com.tw/Images/NewShop/ShopDescription/109170/109170-6.jpg)

多模光纖 (Multi Mode)

![多模光纖](http://images.100y.com.tw/Images/NewShop/ShopDescription/109170/109170-9.jpg)


**比較項目** | **單模光纖** | **多模光纖**
------------ | ------------ | -------------
中心玻璃芯 | 9 ~ 10μm | 50 ~ 62.5μm
最大傳輸距離 | 幾十公里 | 半公里內
線套顏色 | 黃色 | 藍 & 橘色
線路價格 | 便宜 | 貴
設備價格 | 貴 | 便宜
使用光源 | 激光源 | LED光源


那這樣比較我到底要抉擇什麼的光纖線會比較好?

**實際還是依傳輸距離來決定**


# 2. 光模塊要怎選用?

選用前要先知道現**場使用的光纖類型是 單模 還是 多模**

然後**傳輸的距離**是多遠以及**Switch的設備**選用

那麼我們開始介紹光纖模塊的種類吧

目前我所知道的總共有4個總類

1. 10Gigabit XFP
2. 10Gigabit SFP+
3. Gigabit SFP
4. Fast Ethernet SFP

而目前最常使用到的是 3. Gigabit SFP

那麼這些東西的差異在哪邊?
1. 10Gigabit XFP
    > 需要用到時在介紹了~
2. 10Gigabit SFP+
    > 需要用到時在介紹了~
3. Gigabit SFP (GE, GbE or GigE)
    > 1000-Base (Giga Ethernet) 而這已成主流
4. Fast Ethernet SFP
    > 100-Base (Fast Ethernet) 目前連光模塊都不一定買的到
    
因此我們幾乎都會買1000-Base的MiniGBic (SFP Gbic)
1[MiniGBic](http://www.genb2b.com/UploadFile/ComProImages/be6d9cf9-c0c8-4b03-ba9c-003a11b826a4/201783119493115fd91-da76-4f87-b13e-6025832f2c91_300.jpg)

那之前大家統稱的GBic是舊時代的叫法
GBic的樣子
![GBic](http://www.feisu.com/tw/imgCache/7/7b90a309a297bd2493aa57051aa52bbd.image.550x550.jpg)

接著光模塊還有細分TX、FX、SX、LX、ZX

Ethernet Type | Rate | Transmission Medium | Medium Thpe | Transmission Distance
------------ | ------------ | -------------
100Base-Tx | Two Pairs | Category 5 | 100m
100Base-FX | Multi-Mode Fiber | 62.5μm | 400m(half duplex)
100Base-FX | Single-Mode Fiber | 9μm | 10km
1000Base-SX(850nm laser) | Multi-Mode Fiber| 62.5μm | 275m
1000Base-LX(1310nm laser) | Multi-Mode Fiber| 62.5μm  | 550m
1000Base-LX(1310nm laser) | Single-Mode Fiber| 9μm | 10km
1000Base-ZX(1550nm laser) | Single-Mode Fiber| 9μm  | 70km

# 3. 100M是包含10/100內還是100/1000內?

上面敘述希望有幫到,

那用一台設備來介紹吧這段吧

這是之前碰到的經驗談...

L2網管型高速乙太網路交換器，24端口SFP 100M + 2端口Combo SFP-TP GbE
![pic](http://plus.webdo.com.tw/manager_admin/upload_file/419/14223794191.jpg)

看到24端卡SFP 100M超爽! 價格也很便宜!

結果買回來插上SFP-LX-10-D後結果不通...

明明SFP-LX-10-D是100/1000M阿

應該有支援啊!

其實不然...

100M 其實指的是 100-Base ( Fast Ethernet ) !!!

而實際上有支援的只有最後那2端口 SFP-TP GbE ( Giga Ethernet )...

所以在搭配使用前要先將規格看清楚再選用

而Fast Ethernet目前也有賣啦... 但是要再詢問看看就是了。

我們常配合的Zyxel也有賣


# 4. 總結
