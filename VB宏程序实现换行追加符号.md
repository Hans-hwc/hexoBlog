---
title: VB宏程序，实现换行追加"\\"符号
categories: 
- Excel
tags:
- excel
- vb
---
#### 关于
有这样一个场景，有一次，公司一个同事说，excel表格中，想在每行换行的地方追加"\\\\"符号，以便该excel表格在导入jira系统的时候，该符号会被系统识别为换行符，方便阅读。于是乎有了下面的研究成果。

#### 完整的vb宏程序
1.打开vb宏编辑窗口，可使用快捷键Alt+F11打开，然后粘贴下面程序。下面的代码可以实现，在你选择的区域，运行宏，则该区域上，凡是换行符的位置都会追加上"\\\\"符号。
```
Sub AppendToSpritOnEnterRight()
Dim c As Range
Dim StaR As String
Dim posStr As String
Dim i As Long
Dim resultStr, cacheStr As String
Dim lastI As Long

For Each c In Selection
    StaR = c.Value
    
    posStr = ""
    cacheStr = ""
    resultStr = ""
    lastI = 0
    
    For i = 1 To Len(StaR)
        posStr = Mid(StaR, i, 1)
        If posStr = Chr(10) Then '拼接字符串\\
            cacheStr = Mid(StaR, lastI + 1, i - 1 - lastI) & "\\" & Chr(10)
            resultStr = resultStr + cacheStr
            lastI = i
            //MsgBox resultStr
        End If
    Next i
    
    cacheStr = Mid(StaR, lastI + 1, Len(StaR) - lastI)
    resultStr = resultStr + cacheStr
    
    c.Value = resultStr
Next

End Sub
```

2.补充几点
常用快捷键：
Alt+Entry：换行
Alt+F11：打开程序窗口
F5：打开运行宏窗口

函数：
Mid(String,start[,Length])
String - 必需的参数。输入从中返回指定数量的字符的字符串。
Start - 必需的参数。 一个整数，它指定了字符串的起始位置。
Length - 必需的参数。 一个整数，指定要返回的字符数。
注意：Start需要从1开始。

