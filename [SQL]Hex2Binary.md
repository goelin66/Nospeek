```T-SQL
use MyDB
go

--dbo.HexToBinary(value)

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
