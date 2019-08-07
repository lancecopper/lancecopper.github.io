---
title: Hello World
---

## 引文
没啥好说的，就是想整理个快速入门手册。

## 参考资料
[jinjia2模板文档](http://jinja.pocoo.org/docs/2.10/


## Basic API Usage

* jinja2目前已经加入对python version3的支持

``` python
>>> from jinja2 import Template
>>> template = Template('Hello {{ name }}!')
>>> template.render(name='lancecopper')
'Hello lancecopper!'
```

```python
from jinja2 import Environment, PackageLoader, select_autoescape
env = Environment(
    loader=PackageLoader('yourapplication', 'templates'),
    autoescape=select_autoescape(['html', 'xml'])
)
```














