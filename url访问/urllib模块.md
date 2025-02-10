# urllib

urllib 是 Python 标准库中用于处理 URL 的模块。它包含四个子模块：request、error、parse 和 robotparser



## 什么是Urllib

Urllib是python内置的HTTP请求库 包括以下模块:

| urllib.request     | 请求模块           |
| ------------------ | ------------------ |
| urllib.error       | 异常处理模块       |
| urllib.parse       | url解析模块        |
| urllib.robotparser | robots.txt解析模块 |

## request

`urllib`的`request`模块可以非常方便地抓取URL内容，也就是发送一个请求到指定的页面，然后返回HTTP的响应

### urlopen()

`urlopen(url[, data][, timeout])` 是 `urllib.request` 中最基本的函数，用于打开一个 URL，并返回一个类似于文件对象的响应对象。

语法和参数解释

```python
urlopen(url[, data][, timeout]) -> response
```

- `url`：要打开的 URL。
- `data` (可选)：要发送到服务器的数据。如果提供了数据，请求方法将被设置为 POST。
- `timeout` (可选)：设置超时时间（以秒为单位）。

实例

```python
import urllib.request

# 写法一：使用 urlopen 打开 URL 并读取内容
with urllib.request.urlopen('http://httpbin.org/get') as response:
    html = response.read().decode('utf-8')
    print(html)
#写法二
response = request.urlopen("http://httpbin.org/get")
print('Status:', response.status, response.reason)
print(response.read())

# 使用 urlopen 发送 POST 请求
import json
data = {'key1': 'value1', 'key2': 'value2'}
data = json.dumps(data).encode('utf-8')
with urllib.request.urlopen('http://httpbin.org/post', data) as response:
    result = response.read().decode('utf-8')
    print(result)
```

我们可以通过

response.status    获取状态码

response.getheaders()

response.getheader("server")   获取头部信息

response.read()      获得的是响应体的内容



### Request()

如果我们要想模拟浏览器发送GET请求，就需要使用`Request`对象，通过往`Request`对象添加HTTP头，我们就可以把请求伪装成浏览器。

`Request(url[, data][, headers][, origin_req_host][, unverifiable])` 用于创建一个 Request 对象，用于向服务器发送请求。

语法和参数解释

```python
Request(url[, data][, headers][, origin_req_host][, unverifiable]) -> request
```

- `url`：要请求的 URL。
- `data` (可选)：要发送到服务器的数据。
- `headers` (可选)：一个字典，包含要添加到请求头的键值对。
- `origin_req_host` (可选)：用于识别请求的来源主机的字符串。
- `unverifiable` (可选)：一个布尔值，指示是否可以验证请求的来源。

实例

```python
import urllib.request

# 创建一个 Request 对象并发送 GET 请求
req = urllib.request.Request('https://www.example.com')
with urllib.request.urlopen(req) as response:
    html = response.read().decode('utf-8')
    print(html)

# 创建一个 Request 对象并发送 POST 请求
import json
data = {'key1': 'value1', 'key2': 'value2'}
data = json.dumps(data).encode('utf-8')
req = urllib.request.Request('https://www.example.com/api', data, {'Content-Type': 'application/json'})
with urllib.request.urlopen(req) as response:
    result = response.read().decode('utf-8')
    print(result)
```