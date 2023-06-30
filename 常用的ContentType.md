```html
Content-Type:	text/html;charset=UTF-8
```

- 不区分大小写，但为了规范，Content和Type首字母大写，值全部小写

值由主类型和子类型组成，有的值包含附加参数，如字符编码等信息，如 `text/html; charset=utf-8`。

# 常见的Content-Type

| Content-Type             | 作用                                           |
| ------------------------ | ---------------------------------------------- |
| text/plain               | 纯文本类型，用于传输普通文本数据。             |
| text/html                | HTML 文档类型，用于传输网页内容。              |
| text/javascript          | JAVASCRIPT脚本文件                             |
| text/css                 | CSS样式文件                                    |
| application/json         | JSON 数据类型，用于传输结构化数据。            |
| application/xml          | XML 数据类型，用于传输可扩展标记语言数据。     |
| application/octet-stream | 二进制数据类型，用于传输任意二进制数据。       |
| multipart/form-data      | 用于在 HTTP 请求中传输带有文件上传的表单数据。 |
| image/jpeg               | JPG格式图片                                    |
| image/gif                | GIF动图                                        |
| image/png                | PNG格式图片                                    |
| image/webp               | WEBP格式图片                                   |
| video/mp4                | MP4格式视频                                    |



# 几种语言设置ContentType的方式

在Java中，可以使用Servlet API来设置响应头。以下是一个示例代码片段：

```java
import javax.servlet.http.HttpServletResponse;

// 获取HttpServletResponse对象
HttpServletResponse response = ...;

// 设置Content-Type为"text/plain"
response.setContentType("text/plain");
```



在Node.js中，可以使用`setHeader`方法或`writeHead`方法来设置响应头。以下是一个示例代码片段：

```javascript
const http = require('http');

http.createServer((req, res) => {
  // 设置Content-Type为"text/plain"
  res.setHeader('Content-Type', 'text/plain');
  // 或者使用writeHead方法
  // res.writeHead(200, {'Content-Type': 'text/plain'});

  // 其他处理逻辑...

  res.end('Hello, World!');
}).listen(3000);
```



在Python中，可以使用不同的Web框架来设置响应头。以下是使用Flask框架的示例代码片段：

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    # 设置Content-Type为"text/plain"
    return 'Hello, World!', 200, {'Content-Type': 'text/plain'}
```

以上是在Java、Node.js和Python中设置HTTP响应头Content-Type的几种常见方法。具体的实现方式可能会根据你使用的框架或库而有所不同。