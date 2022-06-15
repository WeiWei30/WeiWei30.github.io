[官方参考文档](https://docs.python.org/3/reference/datamodel.html)

## dunder method

dunder method是指那些前后都拥有“__”的method，是python中一种特殊的“函数”。如果在类中定义了这些dunder method，就可以不再使用Class.len()，而是采用len(Class)，与python中内置的数据类型保持一致，体现了**python的一致性**，且不同人写的不同的类也可以保持一致。另一方面，**使用dunder method的运行速度是最快的**。

### --repr--和--str--

--repr--的返回值是调试时用的，一行内只有某个变量时会调用--repr--；--str--是调用print()时候输出的。

### 运算符重载

len()、[]都可以看作是一元运算符，可通过dunder method使用；+、-等二元运算符也可以通过dunder method实现，分别为--add--、--sub--等。

## 类的常量属性定义和调用

```python
class FrenchDeck:

	ranks = [str(n) for n in range(2, 11)] + list('JQKA')

	suits = 'spades diamonds clubs hearts'.split()

def __init__(self):
	self._cards = [Card(rank, suit) for suit in self.suits

def __len__(self):
	return len(self._cards)

def __getitem__(self, position):

	return self._cards[position]
```

类的常量属性放在init()的前面，在类内用self.调用他们即可。在类外用FrenchDeck.调用他们。