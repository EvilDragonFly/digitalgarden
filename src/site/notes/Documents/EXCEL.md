---
{"dg-publish":true,"permalink":"/Documents/EXCEL/","noteIcon":""}
---

1. 查看某一列中是否有重复项
```excel
# check which value in col S3 is repeated with col A in sheet
=IF(COUNTIF(Sheet2!A:A,S3)>1,"repeated","not repeated")

=IF(OR(COUNTIF(Sheet1!A:A,S3)>0,COUNTIF(Sheet2!A:A,S3)>0),"repeated,"not repeated")
```


