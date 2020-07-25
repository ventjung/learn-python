# Control Flow

## While
```
a, b = 0, 1
while a < 1000:
    print(a, end=',')
    a, b = b, a+b
```

## If...elif...else, If...in, pass, Built-in (input)
```
x = int(input("Masukkan 1 atau 2: "))
if x == 1:
    pass
elif x == 2:
    print('dua')
else:
    print('bukan satu atau dua')
```

```
x = 'hello'
if 'h' in x:
    print(True)

y = [1, 2, 3]
if 1 in y:
    print(True)
```

```
# pass statement
while True:
    pass

class MyEmptyClass:
    pass

def myEmptyFunction():
    pass
```

## For...in, Iterable, Built-in (range, sum), break, else, continue, Loop Technique
```
# for
for n in range(3):
    print(n)
```

```
# sum
sum(range(4)) # 6
```

```
# range
range(3) # 0, 1, 2
range(5, 10) # 5, 6, 7, 8, 9
range(0, 10, 3) # 0, 3, 6, 9
range(-10, -100, -30) # -10, -40, -70
```

```
# loop each item of list
a = ['First', 'Second', 'Third']
for i in range(len(a)):
    print(i, a[i])
```

```
# break, else (loop exhausted)
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, 'equals', x, '*', n//x)
            break
    else:
        # loop fell through without finding a factor
        print(n, 'is a prime number')    
```

```
# continue
for num in range(2, 10):
    if num % 2 == 0:
        print("Found an even number", num)
        continue
    print("Found a number", num)
```

```
# Looping Techniques

# loop copy of list, to remove value from original array
numbers = [1, 2, 3, 4, 5]
for n in numbers.copy():
    if(n % 2 == 0):
        numbers.remove(n)

# numbers => [1, 3, 5]

# loop dictionary
knights = {'gallahad': 'the pure', 'robin': 'the brave'}
for k, v in knights.items():
    print(k, v)

# output: 
# gallahad the pure
# robin the brave

# loop with index using enumerate
for i, v in enumerate(['tic', 'tac', 'toe']):
    print(i, v)

# output:
# 0 tic
# 1 tac
# 2 toe

# loop 2 list barengan
questions = ['name', 'quest', 'favorite color']
answers = ['lancelot', 'the holy grail', 'blue']
for q, a in zip(questions, answers):
    print('What is your {0}?  It is {1}.'.format(q, a))

# output: 
# What is your name?  It is lancelot.
# What is your quest?  It is the holy grail.
# What is your favorite color?  It is blue.

```

## Function, Packing-Unpacking, Lambda, Documentation Strings, Annotations

```
# Function, None, Return
def my_function(param = None, *arguments, **keywords):
    print(param)
    for arg in arguments:
        print(arg)
    for kw in keywords:
        print(kw)

def my_special_function(pos_param, /, std_param, *, kwd_param):
    print(pos_param)
    print(std_param)
    print(kwd_param)
    return 100

my_function(1, 2, 3, p1=True, p2=False)
print(my_special_function(1, 2, kwd_param=3))
```

```
# Lambda
anon_function = lambda: 5
print(anon_function())

anon_function_alt = lambda x: x + 1
print(anon_function_alt(10))
```

```
# Packing Unpacking
list(range(3)) # 0, 1, 2 => [0, 1, 2] # pack = iterables to sequence
args = [0, 3] # *args : [0, 3] => 0,3 # unpack = sequence to iterables
list(range(*args))
```

```
# Docstrings
def my_function():
    """Do nothing, but document it.

    No, really, it doesn't do anything.
    """
    pass

print(my_function.__doc__)
```

```
# Annotations
def f(ham: str, eggs: str = 'eggs') -> str:
    pass

print(f.__annotations__)
```

# Exception Handling

```
try:
    pass
    # raise OSError() # uncomment this untuk eksekusi except yang unexpected
    raise ValueError() 
    # comment raise diatas untuk eksekusi else
except ValueError:
    print('value')
except:
    print('unexpected')
else:
    print('else') # else tereksekusi kalau tidak ada exception di try
finally:
    print('finally') # finally akan selalu dieksekusi ada atau tidak exception
```