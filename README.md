# Django搭建博客

## 1. pipevn+django初始化

```bash
pipenv install
pipenv shell
pipenv --venv
pipenv -h
pipenv install django
pipenv run python
pipenv run django-admin startproject blog ./
pipenv run python manage.py runserver
source /Users/yuexiao/.local/share/virtualenvs/blog-mNRaupox/bin/activate
pipenv install flake8 --dev
pipenv run python manage.py runserver
source /Users/yuexiao/.local/share/virtualenvs/blog-mNRaupox/bin/activate
pipenv install black --dev --pre
source /Users/yuexiao/.local/share/virtualenvs/blog-mNRaupox/bin/activate
```

改时区、语言:

```python
LANGUAGE_CODE = "zh-hans"

TIME_ZONE = "Asia/Shanghai"
```

## 2. 新建博客APP

```bash
pipenv run python manage.py startapp blogapp
```

在setting里面 installapp里注册 blogAPP

## 3. 新建数据模型

blogapp/models.py

主要是一对多多对多关系的理解,后续项目的复杂数据库逻辑的设计
