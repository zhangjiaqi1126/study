# HtmlParser

 Python 标准库中用于解析 HTML 文档的模块。它提供了一种简单的方式来解析 HTML 并提取其中的数据。

常用方法：　

| handle_starttag(tag, attrs)    | 处理开始标签，比如<div>；这里的attrs获取到的是属性列表，属性以元组的方式展示 |
| ------------------------------ | ------------------------------------------------------------ |
| handle_endtag(tag)             | 处理结束标签,比如</div>                                      |
| handle_startendtag(tag, attrs) | 处理自己结束的标签，如<img />                                |
| handle_data(data)              | 处理数据，标签之间的文本                                     |
| handle_comment(data)           | 处理注释，<!-- -->之间的文本                                 |

解析HTML文档的流程
当你调用 feed() 方法向 HTMLParser 对象提供HTML数据时，解析器会逐字符读取输入并调用相应的回调方法。例如：

当解析到 <html> 标签时，handle_starttag 方法会被调用。
解析到 </html> 时，handle_endtag 方法会被调用。
在两个标签之间的文本内容（如 Hello, World!）会触发 handle_data 方法。
遇到 <!-- This is a comment --> 时，handle_comment 会被调用。