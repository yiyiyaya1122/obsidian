
# Builtin 
| 函数名        | 功能描述                                                                                                                         | 示例代码                                                                                                                                                          |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sorted()` | 对可迭代对象（如列表、元组等）进行排序，返回一个新的已排序列表，原对象保持不变。可以通过 `key` 参数指定排序的依据，还能通过 `reverse` 参数控制升序（默认，`reverse=False`）或降序（`reverse=True`）排序。 | `python<br>numbers = [3, 1, 4, 1, 5, 9, 2, 6, 5]<br>sorted_numbers = sorted(numbers)<br>print(sorted_numbers)<br>`                                            |
| `map()`    | 对可迭代对象中的每个元素应用指定的函数，返回一个迭代器，该迭代器会生成应用函数后的结果。可以将多个可迭代对象作为参数传入，函数会依次从每个可迭代对象中取元素作为参数进行调用。                                      | `python<br>def square(x):<br> return x ** 2<br>numbers = [1, 2, 3, 4]<br>squared_numbers = map(square, numbers)<br>print(list(squared_numbers))<br>`          |
| `filter()` | 过滤可迭代对象中的元素，返回一个迭代器，该迭代器只包含使指定函数返回 `True` 的元素。函数接收一个可迭代对象作为参数，依次对可迭代对象中的每个元素调用指定函数，根据返回值的布尔结果决定是否保留该元素。                      | `python<br>def is_even(x):<br> return x % 2 == 0<br>numbers = [1, 2, 3, 4, 5, 6]<br>even_numbers = filter(is_even, numbers)<br>print(list(even_numbers))<br>` |

# String

|      方法名       |                      功能描述                       |                                示例代码                                |
| :------------: | :---------------------------------------------: | :----------------------------------------------------------------: |
|   `lower()`    |                 **大写字符转换为小写字符**                 |             `pythonstr1 = "HELLO"print(str1.lower())`              |
|   `upper()`    |                 **小写字符转换为大写字符**                 |             `pythonstr1 = "hello"print(str1.upper())`              |
|   `split()`    |              **指定分隔符将字符串分割成一个列表**               |          `pythonstr1 = "Hello World"print(str1.split())`           |
|   `strip()`    |     **移除字符串首尾的指定字符**（默认为空白字符，包括空格、制表符、换行符等）     |         `pythonstr1 = " Hello World "print(str1.strip())`          |
|   `lstrip()`   |                **移除字符串开头的指定字符**                 |         `pythonstr1 = " Hello World"print(str1.lstrip())`          |
|   `rstrip()`   |                **移除字符串末尾的指定字符**                 |         `pythonstr1 = "Hello World "print(str1.rstrip())`          |
|   `count()`    |             **返回指定子字符串在字符串中出现的次数**              |         `pythonstr1 = "Hello World"print(str1.count("o"))`         |
|    `find()`    |       返回指定子字符串在字符串中首次出现的索引位置，**否则返回 -1**        |       `pythonstr1 = "Hello World"print(str1.find("World"))`        |
|   `index()`    | 返回指定子字符串在字符串中首次出现的索引位置，**否则抛出 `ValueError` 异常** |       `pythonstr1 = "Hello World"print(str1.index("World"))`       |
| `startswith()` |  检查字符串是否以指定的子字符串开头，如果是则返回 `True`，否则返回 `False`   |    `pythonstr1 = "Hello World"print(str1.startswith("Hello"))`     |
|  `endswith()`  |  检查字符串是否以指定的子字符串结尾，如果是则返回 `True`，否则返回 `False`   |     `pythonstr1 = "Hello World"print(str1.endswith("World"))`      |
|  `replace()`   |       将字符串中的指定子字符串替换为另一个子字符串，并返回替换后的新字符串        | `pythonstr1 = "Hello World"print(str1.replace("World", "Python"))` |
|   `center()`   |   返回一个指定宽度的新字符串，原字符串居中显示，两侧用指定的填充字符（默认为空格）填充    |         `pythonstr1 = "Hello"print(str1.center(10, "*"))`          |
|    `join()`    |     将一个可迭代对象（如列表、元组等）中的元素以指定的字符串连接成一个新的字符串      |      `pythonlist1 = ["Hello", "World"]print("-".join(list1))`      |

# Python高级语法

- 装饰器 (`Decorators`)
- 生成器（`Generators`）
- 上下文管理器（`Context Managers`）
- 元类（`Metaclasses`）
- 数据类 (`Dataclasses`)
- 描述符（`Descriptors`）
- 异步（`Async`）


**Reference**
- [[2025-10-24#`Python`高级语法]]