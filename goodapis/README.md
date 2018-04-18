# 怎么设计一个好的API?
## 什么是 Application Programming Inteface?
## 一个好的API有什么样的一些标准?
1. 站在使用者的角度
2. 你用过的最好的产品的UI界面是什么？

## 怎么才算一个好的API?

The Zen of Python, Python之禅

### 1. 够简单
#### 90% 的应用场景都能够覆盖
1. 从一个好的README开始
    - [Python datetimes made easy](https://github.com/sdispater/pendulum)
    - [Requests: HTTP for Humans](https://github.com/requests/requests)
        - [没有对比，就没有伤害](https://gist.github.com/kennethreitz/973705)
    - [Beautiful Soup is a Python library for pulling data out of HTML and XML files](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
2. 了解你的用户
    - [提炼优秀的Use Case](http://python-social-auth-docs.readthedocs.io/en/latest/use_cases.html#)
3. 让设计变得很简洁, 去除冗余信息 
    - Google 主页

    ```python
    # simple
    uk_users = User.objects(country='uk')
    
    # advanced
    Page.objects(__raw__={'tags': 'coding'})
    ```

    - 提供默认选项 
    ```javascript
    history.pushState(null, "", "https://hello.com")
    history.pushState("https://hello.com")
    ```

    - 输入参数应该更加直观
    ```python
    mailer.send(
        to=["someone@example.com"],
        subject="Some subject",
        body="Some body"
    )
    mailer.send(
        to="someone@example.com",
        ...
    )
    ```

    - 避免需要初始化的参数输入

    ```python
    RawConfigParser.readfp(StringIO('my config'))

    RawConfigParser.read_string('my config')
    ```

    - 创建抽象, 从具体到抽象, 从how到what
    
    ![抽象](abstract.png)

    ![画画](painting.jpeg)

    ```python
    @app.task
    def add(x, y):
        return x + y

    html_soup.select('p.my_class')
    ```
    1. 如果出现了leaky of abstraction?
    2. [Complex vs Complicated](https://stackoverflow.com/questions/4568704/what-does-complex-is-better-than-complicated-mean?)

4. Be Pythonic
```python
parser.get(section, option)

parser['section']['option']
```
Python 的魔法方法

### 2. 够灵活

1. 拆分代码粒度, 分离代码职责

```python
print_formatted('Hello world', 'red', 'bold')

print_formatted('Hello world', 'red', 'bold', out=some_file)

print(formatted('Hello world', 'red', 'bold'))
```

[Python Logging 设计](loggin-design.jpg)

2. 增强代码可扩展性

[django_restframework](https://github.com/encode/django-rest-framework/pull/3147)

```python
if self.page_size is None:
    return None

page_size = self.get_page_size(request)
if not page_size:
    return None
```

3. Pythonic
Design Patterns

- Adapter -> DuckTyping

- Strategy -> HoF

```python
person_list.sort(key=lambda x: x.age)
```

```java
Collections.sort(List<T> list, Comparator c)
```

# 最后
An API should make the simple easy, the complex possible and the wrong impossible.
