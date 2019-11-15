# Aplus整合測試紀錄

前言 : 配合測試整合, 搭配後留下些紀錄。

測試內容 :

[1. 前置作業準備](https://github.com/goelin66/Nospeek/new/master#1-%E5%89%8D%E7%BD%AE%E4%BD%9C%E6%A5%AD%E6%BA%96%E5%82%99)

[2. 架構](https://github.com/goelin66/Nospeek/new/master#2-%E6%9E%B6%E6%A7%8B)

[3. 觸發的路徑](https://github.com/goelin66/Nospeek/new/master#3-%E8%A7%B8%E7%99%BC%E7%9A%84%E8%B7%AF%E5%BE%91)

[4. 後續探討](https://github.com/goelin66/Nospeek/new/master#4-%E5%BE%8C%E7%BA%8C%E6%8E%A2%E8%A8%8E)


# 1. 前置作業準備

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

-  A. 請搭配 WebAccess8.4.2以上的版本比較安全

在這個版本以上才有支援

詳細文件如下

![imgage of WebAccess8.4.2 ReleaseNote](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_ChromeKernel_201911151606.jpg)

細節請參考官網的 

[Release Note](https://support.advantech.com/support/DownloadSRDetail_New.aspx?SR_ID=1-1J6QG9J&Doc_Source=Download)

-  B. 凱鴻的程式請準備好

![image of A++_GW](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_A%2B%2BGW_201911151616.png)

接著開啟你的專案

開始玩吧!

下圖為後續呈現樣式目標~

![image of Almsum](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_Almsum_201911151622.jpg)


[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

# 2. 架構

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

BA可以直接在本地點回放影像, 

或者其他電腦透過網頁(IE)瀏覽 BA的人也可以查閱。

![image of silly structure](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_SillyStructure_201911151628.jpg)

其他細項都需要再 BA-PC做調整...

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

# 3. 觸發的路徑

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)


![image of silly structure2](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_SillyStructure2_201911151639.jpg)

就如圖上我說的時間這個戳記是我目前碰到最難處裡的,

一定要戳到那個警報點才能讀取警報時間的紀錄,

目前先做簡單的 Live即可。

問我為什麼?

因為 Live的部分很簡單阿~

只要有 NVR IP、 CAM即可,

再將這些資料藏在警報點內就能完成了~

![image of Tag Deatil](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_TagDetail_201911151650.jpg)

至於 Playback則需要更多的資訊來拼湊使用...

回正軌...

完成後透過 Scr腳本來呼叫

因為我比較笨所以寫了將近 22個腳本來使用

```tcl
# # almsum_CAM01.scr
catch {
    #宣告變數讓警報資料可以塞入
    set ppcamera00 "%TLV(%TALMSUM4 0 [GETVAL %AALMSUMP])"
    
    #將變數塞到站存旗標以便日後判斷
    SETVAL Z_alarm_point1=[GETVAL $ppcamera00]
    
    #如果警報對應攝影機的編號有數值則觸發腳本、沒有則不動作
    if {[GETVAL CAM00]>0 } then {
        #呼叫彈跳 Live的腳本
        SCREXEC almsum_PPCAM.scr
    } else {
        
    }
} err

```

另外還需要增加一些東西來讓畫面更加生動,

讓使用者可以知道這個警報是有搭配影像的。

```tcl
# # almsum.scr
catch {
   #宣告變數讓警報資料可以塞入
   set camera00 "%TLV(%TALMSUM4 0 [GETVAL %AALMSUMP])"
   
   #確認有警報在把
   if {[GETVAL %AALMSUMS(0)]>0} then {
      SETVAL CAM00=[GETVAL [GETVAL $camera00].extva3]
   } else {
      SETVAL CAM00=0
   }
} err
```

當這些東西都完成後即可以彈跳 Live視窗了。


[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

# 4. 後續探討

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

這些功能使用上都是依靠許多人給的建議才刻出來的版型,

基本上語法還可以在更加優化,

但都只是為了展示測試,

現階段只有做到這邊...

至於調整為影像回放的功能,

雖然後續有研究一下文件,

發現可以透過 *.ALMTM來處理...

但這是一條坎坷的路阿, 不知道這家廠商可以配合到怎麼樣的程度...

因擔心自己忘了, 留下一些足跡讓日後有機可循...

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)
