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

BA可以直接在本地點回放影像, 

或者其他電腦透過網頁(IE)瀏覽 BA的人也可以查閱。

![image of silly structure](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_SillyStructure_201911151628.jpg)

其他細項都需要再 BA-PC做調整...

![image of silly structure2](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_SillyStructure2_201911151639.jpg)

就如圖上我說的時間這個戳記是我目前碰到最難處裡的,

一定要戳到那個警報點才能讀取警報時間的紀錄,

雖然可以透過 *.ALMTM來處理...

但想想先做簡單的 Live即可。

目前 Live的部分很簡單

只要有 NVR IP、 CAM即可

再將這些資料藏在警報點內就能完成了~

![image of Tag Deatil](https://github.com/goelin66/Nospeek/blob/master/pic/UsingAplus_TagDetail_201911151650.jpg)

至於 Playback則需要更多的資訊來拼湊使用...

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

```tcl

set tag2 "%TLV(%TALMSUM4 0 [GETVAL %AALMSUMH])"
SETVAL CAM99=[GETVAL [GETVAL $tag2].extva3]
SETVAL SOPTagName=[GETVAL $tag2]
SETVAL SOPTag=[GETVAL [GETVAL $tag2].extvt4]
SETVAL SOPPath=[GETVAL SOP_Addr]/view/[GETVAL SOPTag]^target=pop
# In order to check the local-Tag 
#SETVAL SOPTagv=[GETVAL SOP_Addr][GETVAL SOPTag]#/sop/[GETVAL SOPTag]^target=pop


```
再透過按鈕的方式來達到關閉上一個影像, 

再重新讀取當前的警報資訊確認是否需要彈跳影像。


[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)



[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

# 3. 觸發的路徑

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)



[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)

# 4. 後續探討

[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)



[回首頁](https://github.com/goelin66/Nospeek/new/master#aplus%E6%95%B4%E5%90%88%E6%B8%AC%E8%A9%A6%E7%B4%80%E9%8C%84)
