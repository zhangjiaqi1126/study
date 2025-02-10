Python 中，`collections` 模块提供了一些高级数据结构，用于更方便地处理和操作数据。这些数据结构包括：

1. **Counter**: 用于计数可哈希对象的数量。它返回一个字典子类，其中元素是对象，值是它们出现的次数。

   ```
   from collections import Counter  # 导入 Counter 类
   
   words = ['apple', 'banana', 'apple', 'orange', 'banana']  # 定义一个包含重复元素的列表
   word_counts = Counter(words)  # 使用 Counter 对象统计每个单词出现的次数
   print(word_counts)  # 输出结果：Counter({'banana': 2, 'apple': 2, 'orange': 1})
   
   ```

   

2. **defaultdict**: 是一个字典子类，提供了一个默认值的机制。当你试图访问一个不存在的键时，它会自动创建一个新的键，并将其值设置为默认值。

   ```
   from collections import defaultdict  # 导入 defaultdict 类
   
   student_grades = defaultdict(int)  # 创建一个默认值为 0 的字典
   student_grades['Alice'] = 90  # 为 'Alice' 分配分数
   student_grades['Bob'] = 85  # 为 'Bob' 分配分数
   print(student_grades['Charlie'])  # 访问不存在的键 'Charlie'，由于是 defaultdict，它会自动创建一个新的键并将其值设置为默认值 0
   
   ```

   

3. **OrderedDict**: 是一个有序的字典，它保留了元素插入的顺序。

   使用`dict`时，Key是无序的。在对`dict`做迭代时，我们无法确定Key的顺序。

   如果要保持Key的顺序，可以用`OrderedDict`

   ```
   from collections import OrderedDict  # 导入 OrderedDict 类
   
   ordered_dict = OrderedDict()  # 创建一个空的有序字典
   ordered_dict['a'] = 1  # 添加键值对 'a': 1
   ordered_dict['b'] = 2  # 添加键值对 'b': 2
   ordered_dict['c'] = 3  # 添加键值对 'c': 3
   print(list(ordered_dict.keys()))  # 将有序字典的所有键转换为列表并打印，输出结果：['a', 'b', 'c']
   
   ```

   

4. **deque**: 是一个双端队列，是为了高效实现插入和删除操作的双向列表，适合用于队列和栈

   ```
   from collections import deque  # 导入 deque 类
   
   queue = deque()  # 创建一个空的双端队列
   queue.append('apple')  # 在队列尾部添加元素 'apple'
   queue.append('banana')  # 在队列尾部添加元素 'banana'
   queue.appendleft('orange')  # 在队列头部添加元素 'orange'
   print(queue)  # 打印队列，输出结果：deque(['orange', 'apple', 'banana'])
   
   ```

   

5. **NamedTuple**: 是一个工厂函数，用于创建带有字段名的元组子类。

```
from collections import namedtuple  # 导入 namedtuple 函数

Person = namedtuple('Person', ['name', 'age'])  # 创建一个名为 'Person' 的命名元组，包含两个字段 'name' 和 'age'
person = Person('Alice', 25)  # 创建一个 'Person' 实例，字段 'name' 的值为 'Alice'，字段 'age' 的值为 25
print(person.name)  # 访问 'Person' 实例的 'name' 字段，输出结果：Alice

```

6.`**ChainMap**` 允许你将多个字典或其他映射类型组合成一个单一的视图。在这个视图中，你可以像访问一个普通的字典一样访问所有链表中的键值对。如果在多个字典中存在相同的键，`ChainMap` 会优先返回第一个字典中的值。

```
from collections import ChainMap

# 创建两个字典
dict1 = {'a': 1, 'b': 2}
dict2 = {'b': 3, 'c': 4}

# 使用 ChainMap 将两个字典组合成一个视图
combined_dict = ChainMap(dict1, dict2)

# 访问键值对
print(combined_dict['a'])  # 输出：1
print(combined_dict['b'])  # 输出：2，因为 dict1 中的 'b' 优先于 dict2 中的 'b'
print(combined_dict['c'])  # 输出：4

在上面的例子中，我们首先创建了两个字典 dict1 和 dict2。然后，我们使用 ChainMap 将这两个字典组合成一个视图 combined_dict。最后，我们通过访问 combined_dict 中的键来演示如何使用这个视图。

注意，在访问 combined_dict['b'] 时，返回的是 dict1 中的值 2，而不是 dict2 中的值 3。这是因为在 ChainMap 中，第一个字典的键值对优先于后面的字典。

ChainMap 可以非常方便地用于配置文件、环境变量等多个来源的数据合并，或者在需要根据特定条件选择使用不同字典的情况下。
```

