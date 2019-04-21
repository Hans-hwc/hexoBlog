---
title: html复杂表格
categories: 
- Html
tags:
- html
- css
---
#### 关于
有时候，我们在做web界面显示的时候，经常遇到html复杂表格的编写。主要就是跨列，跨行等。下面分享一个既有跨列又有跨行的复杂表格样例。

#### 具体内容
1.界面效果
![table效果](https://note.youdao.com/yws/public/resource/045283fa941846c3cf8f245a0dd3561b/xmlnote/D3FE80ED6E3E4B0C873DD28CC8E51D3B/9371)

2.html代码
```
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>复杂表格</title>
</head>
<body>
    <center>
        <table width = "60%" border="1">
            <tr>
                <th colspan="2" rowspan="2">跨两行两列</th>
                <th colspan="2">跨两列</th>
            </tr>
            <tr>
                <td>单元格21</td>
                <td>单元格22</td>
            </tr>
            <tr>
                <td>单元格31</td>
                <td>单元格32</td>
                <td>单元格33</td>
                <td>单元格34</td>
            </tr>
            <tr>
                <td>单元格41</td>
                <td>单元格42</td>
                <td>单元格43</td>
                <td>单元格44</td>
            </tr>
        </table>                                                                                                                                                                                                           
    </center>
</body>
</html>
```
