---
{"dg-publish":true,"permalink":"/OperatingSystem/Linux/sed/","noteIcon":"3"}
---

#sed

```bash
# 文件中第6行插入一行
sed -i '6i this is the new line' test.txt
sed -i 's/原始内容/替换内容/\$' 文件名
#替换文件中第6行
sed -i '6s/.*/替换内容/'
sed -n '\$p' 文件名
# 删除文件中的第4行到文件尾
sed -i '4,\$d' 文件名
```