---
{"dg-publish":true,"permalink":"/Documents/EXCEL/","noteIcon":"","created":"","updated":""}
---

#excel
1. 查看某一列中是否有重复项
```excel
# check which value in col S3 is repeated with col A in sheet
=IF(COUNTIF(Sheet2!A:A,S3)>1,"repeated","not repeated")

=IF(OR(COUNTIF(Sheet1!A:A,S3)>0,COUNTIF(Sheet2!A:A,S3)>0),"repeated,"not repeated")
```
2. 查看range内是否存在指定值，并返回对应行内的某一列信息
[vlookup函数](https://zh-cn.extendoffice.com/excel/functions/excel-vlookup-function.html)
[named range](https://exceljet.net/glossary/named-range)
[xlookup search range](https://exceljet.net/formulas/xlookup-match-any-column)
```excel
# VLOOKUP可以搜索多列，但是有一个限制就是需要返回的列必须在lookup_value的右边，因为vlookup默认是从左往右搜索的
=VLOOKUP (lookup_value, table_array, col_index, [range_lookup])
# xlookup的lookup array只能是一列，返回array的行数应与lookup array一致
XLOOKUP(V90,'0529全量盘点机器'!K:K,'0529全量盘点机器'!:C:C)
# 如果想要查看制定range(多列)，而非某一列，可以结合MMULT函数通过矩阵计算来达到
XLOOKUP(1,MMULT(--(RANGE=S22),SEQUENCE(COLUMNS(RANGE),1,1,0)),RETURNARRAY)
```


