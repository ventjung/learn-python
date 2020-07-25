# Untuk comment dalam source code
```
# comment
```

# Untuk nentuin encoding source code
```
# -*- coding: utf-8 -*-
```

# How to Run Python

## Interactive

```
py di CMD
```

## Argument Passing

```
py [filename] [dan argument lainnya]
```

# Statement, Expression, Literal, Operator, Math Operator, Variable Assignment
```
number = 10 + 10 - 10 / 10 * 10 % 10 // (10 ** 10)
# number nilainya 20
```

# Data

## Data Type (built-in type)
Data itu punya tipe, bentuknya bisa literal, atau expression. 
Nanti data yang isinya banyak di python istilahnya sequence, yang biasanya iterable (bisa di loop).

### None
```
type(None)
```

### Number (int, float)
```
type(10)
type(4.5)
```
### Boolean (bool)
```
type(True)
type(False)
```
### String (str) => Sequence, Iterables
```
type('Hello')
```

# Play with String 

```
print(('He' "llo ") * 3 + '\n' + 'It\'s me.\n' + r'C:\Test\Drive')
```
```
output:
Hello Hello Hello
It's me.
C:\Test\Drive
```
```
print('''\
Some long paragraph,
another line of long paragraph
''')
```
```
output:
Some long paragraph,
another line of long paragraph
```

## Sequence, Iterable
Kumpulan data yang bisa diiterasi.

## Indexing, Slicing, Built-in (len, print)
```
word = 'Ventjung'
# indexing
word[0] # V
word[3] # t
word[-1] # g
word[-2] # n
# slicing
# [from:to] 
word[1:3] # en
word[:2] # Ve
word[4:] # jung
word[-2:] # ng
word[:] # Ventjung
# built-in
len(word) # 8
```

# Virtual Environment

```
python3 -m venv my-env
```
