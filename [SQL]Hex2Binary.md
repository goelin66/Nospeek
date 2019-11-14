# HEXtoBINARY

前言 : 因一些機緣巧合下碰到被要求將 Hex拆解成 Binary,

上網爬了一下文章找到後, 

懶得再去收尋因此把這 T-SQL的語法留檔。

 [1. 前制安裝指令](https://github.com/goelin66/Nospeek/blob/master/%5BSQL%5DHex2Binary.md#1-%E5%89%8D%E5%88%B6%E5%AE%89%E8%A3%9D%E6%8C%87%E4%BB%A4)
 
 [2. 測試階段](https://github.com/goelin66/Nospeek/blob/master/%5BSQL%5DHex2Binary.md#2-%E6%B8%AC%E8%A9%A6%E9%9A%8E%E6%AE%B5)

# 1. 前制安裝指令
[回首頁](https://github.com/goelin66/Nospeek/blob/master/%5BSQL%5DHex2Binary.md#hextobinary)
```sql
USE MyDB
GO

CREATE FUNCTION [dbo].[HexToBinary] 
(
  @hex varchar(200) 
)

RETURNS varchar(1000)

AS

BEGIN

  SET @HEX=REPLACE (@HEX,'0','0000')
  set @hex=replace (@hex,'1','0001')
  set @hex=replace (@hex,'2','0010')
  set @hex=replace (@hex,'3','0011')
  set @hex=replace (@hex,'4','0100')
  set @hex=replace (@hex,'5','0101')
  set @hex=replace (@hex,'6','0110')
  set @hex=replace (@hex,'7','0111')
  set @hex=replace (@hex,'8','1000')
  set @hex=replace (@hex,'9','1001')
  set @hex=replace (@hex,'A','1010')
  set @hex=replace (@hex,'B','1011')
  set @hex=replace (@hex,'C','1100')
  set @hex=replace (@hex,'D','1101')
  set @hex=replace (@hex,'E','1110')
  set @hex=replace (@hex,'F','1111')

  RETURN @hex
END

```
[回首頁](https://github.com/goelin66/Nospeek/blob/master/%5BSQL%5DHex2Binary.md#hextobinary)





# 2. 測試階段
[回首頁](https://github.com/goelin66/Nospeek/blob/master/%5BSQL%5DHex2Binary.md#hextobinary)

確認執行完成後

 可以在 MyDB
-  可程式性下
    -  函數
        -  dbo.HexToBinary

依照下方的 T-SQL貼上即可使用,

後續怎麼調整到所需的地方請自行修正。

```sql
USE MyDB
GO

/*--------------測試請將數值寫value內轉換--------------*/
DECLARE @HEX varchar(10)
--修輸入欲轉換的 HEX數值於 ' ' 內
SET @HEX = 'FA'

SELECT dbo.HexToBinary(@HEX) AS 'Binary'

```
[回首頁](https://github.com/goelin66/Nospeek/blob/master/%5BSQL%5DHex2Binary.md#hextobinary)
