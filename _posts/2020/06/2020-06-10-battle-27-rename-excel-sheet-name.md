---
layout: post
title: 'Battle 27: Rename Excel sheet name '
date: '2020-06-10T10:29:00.001-07:00'
author: Chang Liao
tags:
- Python
- Excel
- Pandas
modified_time: '2020-06-10T10:29:52.193-07:00'
blogger_id: tag:blogger.com,1999:blog-3189999653395802666.post-6862721333459495586
blogger_orig_url: https://codedoesnotlie.blogspot.com/2020/06/battle-27-rename-excel-sheet-name.html
---

Here is what I got from an Excel sheet name, there are some unexpected special characteristics. So I designed a simple method to resolve them.

![Figure 1](https://github.com/changliao/changliao.github.io/blob/main/_figure/excel.png?raw=true)

First, we obtained the list of sheet name using the above method:
xl = pd.ExcelFile(sFilename)

    aSheet = xl.sheet_names

Then iterate the names and change the string:
ss=openpyxl.load_workbook(sFilename)
for sSheet in aSheet:
      sSheet_new = sSheet.replace('\xad', '')
      ss_sheet = ss[sSheet]
      ss_sheet.title = sSheet_new
ss.save(sFilename)
(The python indentation may have issue).

Some references:
https://stackoverflow.com/questions/39540789/how-to-rename-the-sheet-name-in-the-spread-sheet-using-python