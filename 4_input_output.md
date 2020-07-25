# Output Formatting

```
year = 2016
event = 'Referendum'
f'Results of the {year} {event}'
```

```
yes_votes = 42_572_654 # bisa pake underscore ga berarti apa2 hanya readability
no_votes = 43_132_495
percentage = yes_votes / (yes_votes + no_votes)
'{:-10} YES votes {:2.2%}'.format(yes_votes, percentage)
```

```
import math
print(f'The value of pi is approximately {math.pi:10.3f}.') # f, float, d, decimal
```

```
print('{0} and {1}'.format('spam', 'eggs')) # spam and eggs
print('{1} and {0}'.format('spam', 'eggs')) # eggs and spam
```

```
print('This {food} is {adjective}.'.format(food='spam', adjective='absolutely horrible')) # This spam is absolutely horrible.
```

```
for x in range(1, 3):
    print('{0:2d} {1:3d} {2:4d}'.format(x, x*x, x*x*x))

# 1   1    1
# 2   4    8
```

```
'1'.rjust(4) # '   1'
'1'.ljust(4) # '1   '
'1'.center(5) # '  1  '
'1'.zfill(5) # '00001'
```

```
import math
print('The value of pi is approximately %5.3f.' % math.pi)
# The value of pi is approximately 3.142.
```

```
# convert ke string menggunakan str atau repr
s = 'Hello, world.'
str(s) # 'Hello, world.'
repr(s) # "'Hello, world.'"
str(1/7) # '0.14285714285714285'
```
```
import datetime 
today = datetime.datetime.now() 
print(str(today)) # 2020-07-23 17:34:38.573012
print(repr(today)) # datetime.datetime(2020, 7, 23, 17, 34, 38, 573012)
```

# Working with Files, Built-in(open), JSON, with...as

```
# ada text mode
f = open('workfile', 'w') # buka filenya, ada mode nya r, w, a, r+ dsb
f.read() # baca seluruh isi file
f.readline() # baca sebaris sebaris (\n)
f.write() # ini buat nulis dari last cursor
f.close() # tutup filenya

# ada binary mode
f = open('workfile', 'rb+')
f.write(b'0123456789abcdef')
f.seek(5) # Go to the 6th byte in the file # 5
f.read(1) # b'5'
f.seek(-3, 2) # Go to the 3rd byte before the end
f.read(1) # b'd'

# untuk mastiin bahwa filenya selalu ke close setelah ga dipakai
with open('workfile') as f:
    read_data = f.read()
```

```
# json
import json
json.dumps([1, 'simple', 'list']) # '[1, "simple", "list"]'

json.dump(x, f) # buat serialize object x ke f text file misalnya
x = json.load(f) # buat deserialize object

```