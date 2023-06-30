# 安装

```python
pip install flask
```



```python
from flask import Flask, request, render_template
import scan_disk
import os

app = Flask(
    __name__,
    static_folder="web-dist/assets",
    static_url_path="/assets",
    template_folder="web-dist",
)


@app.route("/")
def index():
    return render_template("index.html")


@app.route("/directory")
def directory():
    """
    列出文件目录
    """
    root = request.args["root"]
    return scan_disk.get_fold_list(root)


@app.route("/usage")
def usage():
    """
    计算子文件夹占用空间
    """
    root = request.args["root"]
    return scan_disk.calc_usage(root)


if __name__ == "__main__":
    os.system("start http://localhost:5273")
    app.run(port=5273, debug=True)

```

flask服务器只能用于开发测试，因为效率很低

- debug=True 开启热更新

# 请求方式

默认`GET`

```python
@app.route('/login', methods=['GET', 'POST'])
```

```python
@app.get('/login')
def login_get():
    return show_the_login_form()

@app.post('/login')
def login_post():
    return do_the_login()
```

# 查询参数

```python
from flask import request

@app.route('/login', methods=['POST', 'GET'])
def login():
	searchword = request.args.get('key', '')
```

