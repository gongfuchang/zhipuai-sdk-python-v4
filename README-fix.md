# 修改的目的
zhipuai-v4 不兼容 pydantic 1.10.14，导致同时使用 zhipuai-v4 和 pydantic 1.10.14 时，会出现包冲突。
# 修改的地方
- requirements 里修改为 pydantic 1.10.14
- 修改了一些 pydantic 1.10.14 老的方法调用
- _request_opt.py 里的 ClientRequestParam 类加入 config 以跳过 父类的 fields validator:
```python
class ClientRequestParam(pydantic.BaseModel):
    class Config:
        arbitrary_types_allowed = True
```
# 使用方式
```shell
$ git clone xxxx
$ pip install -r requirements.txt
```
build wheel package
```shell
$ pip install setuptools wheel
$ python setup.py sdist bdist_wheel
```
在你的工程下安装 wheel 包
```shell
$ pip uninstall zhipuai
$ pip install dist/zhipuai-0.0.1-py3-none-any.whl
```
