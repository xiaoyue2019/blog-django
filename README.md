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

## 4. 数据库操作

```python
from blogapp.models import Tag, Post, Category
from django.utils import timezone
from django.contrib.auth.models import User

c = Category(name="category test")
t = Tag(name="Tag test")

c.save()
t.save()
print("分类、标签创建完毕")

user = User.objects.get(username="xiaoyue")
c = Category.objects.get(name="category test")

p = Post(
    title="title test",
    body="body test",
    created_time=timezone.now(),
    modified_time=timezone.now(),
    category=c,
    author=user,
)
p.save()
print("文章创建完毕")

c = Category.objects.get(name="category test")
c.name = "category test new"
c.save()
print("修改后的category为：{}".format(Category.objects.all()))

p = Post.objects.get(title="title test")
p.delete()
print("删除成功")
```

创建账号

```bash
pipenv run python manage.py createsuperuser
```

制造迁移文件、迁移数据库

```bash
pipenv run python manage.py makemigrations
pipenv run python manage.py migrate
```

### 5. 视图和模板

1. templates下更改dir[]: "DIRS": [os.path.join(BASE_DIR, "templates")]
2. 主URL配置：path("", include("blogapp.urls"))
3. appURL配置：

    ```python
    from django.urls import path

    from . import views

    urlpatterns = [
        path("", views.index, name="index"),
    ]
    ```

4. 更改视图：

    ```python
    from django.shortcuts import render


    def index(request):
        return render(
            request, "blog/index.html", context={"title": "我的博客首页", "welcome": "欢迎访问我的博客首页"}
        )
    ```

Django开发流程：
    1. 配置APP中的url.py使其与视图绑定
    2. 在工程url.py中引入
    3. 编写视图
    4. 在setting中引入模板

做不下去了，前后端不分离真的难受死了，这辈子不想搞前端啊啊啊啊啊啊
