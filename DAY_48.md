# DAY48 深入研究pandas  
## Pandas
* **Pandas概念**：Pandas是在NumPy基础上建立的新程序库，提供了一种高效的DataFrame数据结构。其中的DataFrame是一种带行标签和列标签、支持相同类型数据和缺失值的多维数组。   
* Pandas的三个基本数据结构：Series、DataFrame和Index。
# Pandas基本数据结构
1、Series对象
* 其为一个带索引数据构成的一维数组，可以用一个数组创建Series对象。   
代码如下：
```python
data = pd.Series([0.25, 0.5, 0.75, 1.0])
print(data)
print('values:', data.values)
print('index:', data.index)
print('data[1]:', data[1])
print('data[1:3]:',data[1:3])
输出：
data[1]: 0.5
data[1:3]: 1    0.50
2    0.75
dtype: float64
```

* Series作为字典使用
字典是一种将任意键映射到一组任意值的数据结构，而Series对象其实是一种将类型键映射到一组类型值的数据结构。   
```python
import pandas as pd

population_dict = {'California': 38332521,
 'Texas': 26448193,
 'New York': 19651127,
 'Florida': 19552860,
 'Illinois': 12882135}
 population = pd.Series(population_dict)
print('population:\n', population)
输出为：
population:
 California    38332521
Texas         26448193
New York      19651127
Florida       19552860
Illinois      12882135
dtype: int64
```
2、DataFrame对象  
DataFrame：既可以作为一个通用型NumPy数组，也可以看作特殊的Python字典。   
* DataFrame作为Numpy数组使用
 ```python
 import pandas as pd

population_dict = {'California': 38332521,
                   'Texas': 26448193,
                   'New York': 19651127,
                   'Florida': 19552860,
                   'Illinois': 12882135}
population = pd.Series(population_dict)
area_dict = {'California': 423967, 'Texas': 695662, 'New York': 141297,
             'Florida': 170312, 'Illinois': 149995}
area = pd.Series(area_dict)

states = pd.DataFrame({'population': population,
                       'area': area})
print('states:\n', states)

# 索引功能
print('states.index:\n', states.index)  # 行信息
print('states.columns:\n', states.columns)  # 列信息
输出：
states:
             population    area
California    38332521  423967
Texas         26448193  695662
New York      19651127  141297
Florida       19552860  170312
Illinois      12882135  149995
states.index:
 Index(['California', 'Texas', 'New York', 'Florida', 'Illinois'], dtype='object')
states.columns:
 Index(['population', 'area'], dtype='object')
 ```
* 几种构建DataFrame的方式
```python
第一种由单个序列组成，接上输入：
a = pd.DataFrame(population, columns=['population'])
print(a)
输出：
            population
California    38332521
Texas         26448193
New York      19651127
Florida       19552860
Illinois      12882135
第二种由列表创建一些数据，输入：
import pandas as pd

data = [{'a': i, 'b': 2 * i}
        for i in range(3)]
a = pd.DataFrame(data)
print(a)
输出：
   a  b
0  0  0
1  1  2
2  2  4
这里的话，即使使用的列表缺少一些值，输出也会用“NaN”补充  

第三种由一系列对象的字典创建，即label 1.4  

第四种由二维数组加索引等创建，输入：
import pandas as pd
import numpy as np

a = pd.DataFrame(np.random.rand(3, 2),
             columns=['foo', 'bar'],
             index=['a', 'b', 'c'])
print(a)  
输出:
        foo       bar
a  0.814909  0.160992
b  0.174402  0.305773
c  0.395690  0.016511
```
3、 缺省值  
* 处理缺失值None：如果在一个没有值的数组中执行sum()或min()的聚合，通常会得到一个错误。此外，整数和None之间的加法是未定义的，所以会产生错误    
* isnull()判断数据是否是无效值，是返回True,否返回False;.notnull()用法相反   
* 填充缺省值
```python
import numpy as np
import pandas as pd

data = pd.Series([1, np.nan, 2, None, 3], index=list('abcde'))
print(data.fillna(0))               # 用0填充缺失值
print(data.fillna(method='ffill'))  # 用缺失值的上一个数填充
print(data.fillna(method='bfill'))  # 用缺失值的后一个数进行填充
```


