# List

```
numbers = [1, 2, 3, 4, 5] + [6, 7, 8]
# indexing
numbers[0] # 1
numbers[3] # 4
numbers[-1] # 5
numbers[-2] # 4
# slicing (return new list)
# [from:to] 
numbers[1:3] # [2, 3]
numbers[:2] # [1, 2]
numbers[4:] # [5, 6, 7, 8]
numbers[-2:] # [7, 8]
numbers[:] # [1, 2, 3, 4, 5, 6, 7, 8] (shallow copy)
# built-in len
len(numbers) # 8
# item assignment
numbers[0] = 99 # [99, 2, 3, 4, 5, 6, 7, 8]
numbers[2:6] = [100, 101] # [99, 2, 100, 101, 7, 8] => index 2-5 (nilai 3-6) dislice, kemudian diselipin 100 dan 101
numbers.append(9) # [99, 2, 100, 101, 7, 8, 9]
numbers[0:4] = [] # [7, 8, 9]
numbers[:] = [] # []
# nesting, access nested item
my_list = [True, 1, 'A', ['hello', 'world']]
my_list[3][0] # hello
```

```
# del statement
a = [-1, 1, 66.25, 333, 333, 1234.5]
del a[0] # a => [1, 66.25, 333, 333, 1234.5]
del a[2:4] # => [1, 66.25, 1234.5]
del a[:] # => []
del a # => a dihapus
```

```
# Append, Extend, Insert, Remove, Pop, Clear
numbers = [1, 2]
numbers.append(3) # [1, 2, 3] add new item at the end of list
numbers.extend([4, 5]) # [1, 2, 3, 4, 5] extend list with new iterables
numbers.insert(2, 2.5) # [1, 2, 2.5, 3, 4, 5] insert value 2.5 at index 2
numbers.remove(2.5) # [1, 2, 3, 4, 5] remove first found value
numbers.pop(0) # pop(index) => index ke 0 yang akan dipop. return value => 1, numbers => [2, 3, 4, 5]
numbers.pop() # index terakhir yang akan dipop. return value => 5, numbers => [2, 3, 4]
numbers.clear() # remove all items, numbers => []
```

```
# Index, Count
numbers = [1, 1, 2, 2, 3, 3]
numbers.index(3) # return 4 karena pertama ketemu
numbers.count(1) # return 2 karena ada 2 buah angka 1
```

```
# Sort, Reverse, Copy
numbers = [5, 3, 2, 4, 1]
numbers.sort() # numbers => [1, 2, 3, 4, 5]
numbers.reverse() # numbers => [5, 4, 3, 2, 1]
new_numbers = numbers.copy() # new_numbers => [5, 4, 3, 2, 1]
```

```
# Use List as Queue
from collections import deque
numbers = deque([1, 2, 3, 4, 5])
numbers.popleft() # return value => 1
print(list(numbers)) # numbers => [2, 3, 4, 5]
```

# Tuple 

```
# Tuple

t = 100, 200, 'hello' # values separated by commas, (100, 200, 'hello')
x, y, z = t # sequence unpacking => x = 100, y = 200, z = 'hello'
t[0] # 100
t[0] = 300 # error, karena immutable
u = t, (1, 2, 3) # bisa nested, ((100, 200, 'hello'), (1, 2, 3))

# Tuple's Special Rule

empty = () # empty tuple mesti pake kurung
singleton = 'hello', # tuple dengan 1 item mesti ada komanya

```

# Set

```
basket = {'apple', 'orange', 'apple', 'pear', 'orange', 'banana'}
print(basket) # show that duplicates have been removed
a = set('abracadabra')
b = set('alacazam')
a                                  # unique letters in a
a - b                              # letters in a but not in b
a | b                              # letters in a or b or both
a & b                              # letters in both a and b
a ^ b                              # letters in a or b but not both
```

# Dictionaries

```
tel = {'jack': 4098, 'sape': 4139} # tel => {'jack': 4098, 'sape': 4139}
tel['guido'] = 4127 # tel => {'jack': 4098, 'sape': 4139, 'guido': 4127}
del tel['sape']

dict([('sape', 4139), ('guido', 4127), ('jack', 4098)]) # {'sape': 4139, 'guido': 4127, 'jack': 4098}
{x: x**2 for x in (2, 4, 6)} # {2: 4, 4: 16, 6: 36}
dict(sape=4139, guido=4127, jack=4098) # {'sape': 4139, 'guido': 4127, 'jack': 4098}
```

# List Comprehensions

```
squares = list(map(lambda x: x**2, range(5))) # squares => [0, 1, 4, 9, 16]
# equivalent to
squares = [x**2 for x in range(5)] # squares => [0, 1, 4, 9, 16]

[(x, y) for x in [1,2] for y in [3,4] if x != y] => [(1, 3), (1, 4), (2, 3), (2, 4)] # list of two tupples
# equivalent to
combs = []
for x in [1,2]:
    for y in [3,4]:
        if x != y:
            combs.append((x, y))

matrix = [
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
]
[[row[i] for row in matrix] for i in range(4)] # [[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]

# vec = [[1,2,3], [4,5,6], [7,8,9]]
# print([y for x in vec for y in x])
```

# Class

```
class MyClass:
    """A simple example class"""
    i = 12345 # shared property

    # init ini akan dieksekusi pas kita instantiate class ini
    def __init__(self, p1): # ini sebetulnya ga mesti self, tapi linter udah bikin self ini habit
        self.a = 10 # ini contoh nambahin property tertentu aja
        self.p = p1

    def f(self):
        return 'hello world'

x = MyClass('arg1')
y = MyClass('arg1')
print(x.a) # 10
print(x.p) # arg1 
print(x.i) # 12345
print(x.f()) # hello world
```

```
class Dog:
    name = 'dogi'
    tricks = []             # mistaken use of a class variable
    def add_trick(self, trick):
        self.tricks.append(trick)

d = Dog()
e = Dog()
d.name = 'new name' # name dari instance akan diprioritaskan daripada name dari shared data
print(d.name)
print(e.name)
d.add_trick('roll over')
e.add_trick('play dead')
print(d.tricks) # unexpectedly shared by all dogs ['roll over', 'play dead']
```

```
class Parent1:
    pass

class Parent2:
    pass

class MyClass(Parent1, Parent2): # python support multiple inheritance
    __private = 10 # otomatis jadi _MyClass__private, di python ga ada private variable

x = MyClass()
print(x._MyClass__private) # 10

x.name = 'Josep' # bisa nambah property on the fly
print(x.name)
```

```
# Iterator
class Reverse:
    """Iterator for looping over a sequence backwards."""
    def __init__(self, data):
        self.data = data
        self.index = len(data)

    def __iter__(self):
        return self

    def __next__(self):
        if self.index == 0:
            raise StopIteration
        self.index = self.index - 1
        return self.data[self.index]

rev = Reverse('spam')
iter(rev) # buat ngecek apakah iterable atau bukan misalnya iter(range(3))
for char in rev: # si rev ini disini udah jadi iterable dan bisa di for...in
    print(char)
```

### Generator

```
def reverse(data):
    for index in range(len(data)-1, -1, -1): # ini maksudnya dari data length - 1 (3), sampai sebelum -1 berarti sampai 0, berkurang 1 setiap step
        yield data[index]
        
for char in reverse('golf'):
    print(char)
```

```
sum(i*i for i in range(5)) # 0 1 4 9 16 => 30
```