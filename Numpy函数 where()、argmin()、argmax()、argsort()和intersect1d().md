## 准备工作

### 导入numpy



```python
import numpy as np
```

### 示例数据

本文以二分类任务为例，通常我们的model会输出预测的概率，得到概率后需要进行后续的处理，比如：

•根据阈值，将概率大于某个阈值的label设置为1，小于阈值的设置为0•在模型诊断过程中，找出满足某些条件的样本

本文使用的示例数据如下：



```python
predict_prob = np.array([0.1,0.3,0.7,0.4,0.9])
```

## where()

np.where() 方法可以帮助我们找到array中满足条件的元素的位置。现在我们可以使用np.where()找出所有预测概率大于0.5的的元素了：



```python
predict_prob = np.array([0.1,0.3,0.7,0.4,0.9])np.where(predict_prob > 0.5)# output：array([2, 4]),)
```

> 如果我们想将所有概率大于0.5的元素替换为1，否则替换为0，该怎么做呢？

一个**简单粗暴的方式**是先用上面的方法分别找出array中概率大于或者小于0.5的索引，然后再对这些位置的元素重新赋值。

其实，np.where() 一个函数就能完成所有的操作，只需要添加两个参数：

•第一个参数是满足条件替换的值•第二个参数是不满足条件替换的值



```python
predict_prob = np.array([0.1,0.3,0.7,0.4,0.9])np.where(predict_prob > 0.5, 1, 0)# output: array([0, 0, 1, 0, 1])
```

## argmin()、argmax()、argsort()

np.argmin()、np.argmax()方法会返回array中最小或最大的元素索引，对示例数据运行结果如下：



```python
predict_prob = np.array([0.1,0.3,0.7,0.4,0.9])
np.argmax(predict_prob)# output: 4np.argmin(predict_prob)# output: 0
```

> 我们成功找到了array中最大最小的元素索引，那怎样找到前n个最大的或最小的值呢？

**现在该轮到np.sort()上场了**



```python
predict_prob = np.array([0.1,0.3,0.7,0.4,0.9])np.argsort(predict_prob)# output: array([0, 1, 3, 2, 4])
```

np.argsort()方法还支持多维数据的排序，感兴趣的可以自行查看Numpy官方文档[1]

## intersect1d()

intersect1d()要做的是，它会找出两个array中的交集，这个函数和前面的几个函数不同，返回的不是索引位置，而是array中的实际值。

本函数我们使用新的**示例数据：**



```python
arr1 = np.array([1,2,4,4,6])arr2 = np.array([2,3,4,5,6])
```

现在，我们可以使用intersect1d()找出两个数组共同的元素了：



```python
np.intersect1d(arr1, arr2)# output: array([2, 4, 6])
```