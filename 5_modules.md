# Standard Library

```
import os
dir(os) # nampilin semua fungsi dari modul
help(os) # nampilin manual dari module docstring

os.getcwd() # Return the current working directory
os.chdir(r'c:\users\home') # Change current working directory
os.system('mkdir today') # Run the command mkdir in the system shell

import shutil
shutil.copyfile('a.txt', 'b.txt') # copy file
shutil.move('a.txt', r'c:\users\home\desktop') # move file

import glob
glob.glob('*.py') # glob buat searching ['fibo.py', 'python.py']

import sys
print(sys.argv) # nampilin argument kalau dipanggil pake py python.py 1 2 3, dst
sys.stderr.write('Warning, log file not found starting a new one\n') # buat nampilin error message
sys.exit() # buat terminate script

import re
re.findall(r'\bf[a-z]*', 'which foot or hand fell fastest')
re.sub(r'(\b[a-z]+) \1', r'\1', 'cat in the the hat')

import math
math.cos(math.pi / 4)
math.log(1024, 2)

import random
random.choice(['apple', 'pear', 'banana'])
random.sample(range(100), 10) # sampling without replacement
random.random() # random float
random.randrange(6) # random integer chosen from range(6)

import statistics
data = [2.75, 1.75, 1.25, 0.25, 0.5, 1.25, 3.5]
statistics.mean(data)
statistics.median(data)
statistics.variance(data)
# https://scipy.org

# internet access

from urllib.request import urlopen
with urlopen('http://tycho.usno.navy.mil/cgi-bin/timer.pl') as response:
    for line in response:
        line = line.decode('utf-8')  # Decoding the binary data to text.
        if 'EST' in line or 'EDT' in line:  # look for Eastern Time
            print(line)

import smtplib
server = smtplib.SMTP('localhost')
server.sendmail('soothsayer@example.org', 'jcaesar@example.org',
"""To: jcaesar@example.org
From: soothsayer@example.org

Beware the Ides of March.
""")
server.quit()

# dates are easily constructed and formatted
from datetime import date
now = date.today()
now

now.strftime("%m-%d-%y. %d %b %Y is a %A on the %d day of %B.")

# dates support calendar arithmetic
birthday = date(1964, 7, 31)
age = now - birthday
age.days # ngitung sampai hari ini udah berapa  hari hidup

# compression
import zlib
s = b'witch which has which witches wrist watch'
len(s)
t = zlib.compress(s)
len(t)
zlib.decompress(t)
zlib.crc32(s)

# timer untuk ngukur performance

from timeit import Timer
Timer('t=a; a=b; b=t', 'a=1; b=2').timeit()
Timer('a,b = b,a', 'a=1; b=2').timeit()

# doctest

def average(values):
    """Computes the arithmetic mean of a list of numbers.

    >>> print(average([20, 30, 70]))
    40.0
    """
    return sum(values) / len(values)

import doctest
doctest.testmod()   # automatically validate the embedded tests

# unit test

import unittest

class TestStatisticalFunctions(unittest.TestCase):

    def test_average(self):
        self.assertEqual(average([20, 30, 70]), 40.0)
        self.assertEqual(round(average([1, 5, 7]), 1), 4.3)
        with self.assertRaises(ZeroDivisionError):
            average([])
        with self.assertRaises(TypeError):
            average(20, 30, 70)

unittest.main()  # Calling from the command line invokes all tests

# repr
import reprlib
reprlib.repr(set('supercalifragilisticexpialidocious'))

import pprint
t = [[[['black', 'cyan'], 'white', ['green', 'red']], [['magenta',
    'yellow'], 'blue']]]
pprint.pprint(t, width=30)

import textwrap
doc = """The wrap() method is just like fill() except that it returns
a list of strings instead of one big string with newlines to separate
the wrapped lines."""
print(textwrap.fill(doc, width=40))

import locale
locale.setlocale(locale.LC_ALL, 'English_United States.1252')
conv = locale.localeconv() # get a mapping of conventions
x = 1234567.8
locale.format("%d", x, grouping=True) # '1,234,567'
locale.format_string("%s%.*f", (conv['currency_symbol'],
                     conv['frac_digits'], x), grouping=True) # '$1,234,567.80'

from string import Template
t = Template('${village}folk send $$10 to $cause.')
t.substitute(village='Nottingham', cause='the ditch fund')

t = Template('Return the $item to $owner.')
d = dict(item='unladen swallow')
t.substitute(d) # error
t.safe_substitute(d) # ga error

# buat baca 3 file header dari sebuah zip file, tanpa pake builtin zip (binary data)
import struct
with open('myfile.zip', 'rb') as f:
    data = f.read()
start = 0
for i in range(3): # show the first 3 file headers
    start += 14
    fields = struct.unpack('<IIIHH', data[start:start+16])
    crc32, comp_size, uncomp_size, filenamesize, extra_size = fields
    start += 16
    filename = data[start:start+filenamesize]
    start += filenamesize
    extra = data[start:start+extra_size]
    print(filename, hex(crc32), comp_size, uncomp_size)
    start += extra_size + comp_size     # skip to the next header

# multithreading
import threading, zipfile
class AsyncZip(threading.Thread):
    def __init__(self, infile, outfile):
        threading.Thread.__init__(self)
        self.infile = infile
        self.outfile = outfile

    def run(self):
        f = zipfile.ZipFile(self.outfile, 'w', zipfile.ZIP_DEFLATED)
        f.write(self.infile)
        f.close()
        print('Finished background zip of:', self.infile)

background = AsyncZip('mydata.txt', 'myarchive.zip')
background.start()
print('The main program continues to run in foreground.')
print('Main program is waiting until background was done.')
background.join()    # Wait for the background task to finish
print('Main program waited until background was done.')

# logging
import logging
# logging.basicConfig(level=logging.DEBUG, filename='app.log', filemode='w', format='%(name)s - %(levelname)s - %(message)s')
logging.basicConfig(filename='app.log', filemode='w', format='%(name)s - %(levelname)s - %(message)s')
logging.debug('Debugging information')
logging.info('Informational message')
logging.warning('Warning:config file %s not found', 'server.conf')
logging.error('Error occurred')
logging.critical('Critical error -- shutting down')

# weak reference
import weakref, gc
class A:
    def __init__(self, value):
        self.value = value
    def __repr__(self):
        return str(self.value)

a = A(10)                   # create a reference
d = weakref.WeakValueDictionary()
d['primary'] = a            # does not create a reference
d['primary']                # fetch the object if it is still alive

del a                       # remove the one reference
gc.collect()                # run garbage collection right away

d['primary']                # entry was automatically removed

# array, homogeneus, two byte unsigned binary numbers (typecode "H") rather than the usual 16 bytes
from array import array
a = array('H', [4000, 10, 700, 22222])
sum(a)

# deque as sampled before

# bisect
import bisect
scores = [(100, 'perl'), (200, 'tcl'), (400, 'lua'), (500, 'python')]
bisect.insort(scores, (300, 'ruby'))
bisect.insort(scores, (300, 'suby')) # insort spt biasa lexicographical
scores

# heap (terkecil selalu di index 0 ngurut dst)
from heapq import heapify, heappop, heappush
data = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
heapify(data)                      # rearrange the list into heap order
heappush(data, -5)                 # add a new entry
[heappop(data) for i in range(3)]  # fetch the three smallest entries

# decimal (floating point)
from decimal import *
round(Decimal('0.70') * Decimal('1.05'), 2)
round(.70 * 1.05, 2)

Decimal('1.00') % Decimal('.10')
1.00 % 0.10
sum([Decimal('0.1')]*10) == Decimal('1.0')
sum([0.1]*10) == 1.0

getcontext().prec = 36
Decimal(1) / Decimal(7)
```

# Modules, Package

## Modules

```
# fibo.py

def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

def fib2(n):   # return Fibonacci series up to n
    result = []
    a, b = 0, 1
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result
```

```
import fibo
fibo.fib(1000)
fibo.fib2(100)
```

```
from fibo import fib, fib2 # buat import nama tertentu aja
from fibo import * # buat import semua (kecuali yang ada _ nya)
from fibo import fib as fibonacci # buat bikin alias si fib
```

Cara Run Module, Built-in (dir)
```
# kita mau bisa run modul kita seperti ini
python fibo.py <arguments>

# tambahin ini ke fibo.py
if __name__ == "__main__":
    import sys
    fib(int(sys.argv[1]))

# sekarang bisa dijalanin seperti ini : 
python fibo.py 50 # output: 0 1 1 2 3 5 8 13 21 34
```

## Packages

```
sound/                          Top-level package
      __init__.py               Initialize the sound package
      formats/                  Subpackage for file format conversions
              __init__.py
              wavread.py
              wavwrite.py
              aiffread.py
              aiffwrite.py
              auread.py
              auwrite.py
              ...
      effects/                  Subpackage for sound effects
              __init__.py
              echo.py
              surround.py
              reverse.py
              ...
      filters/                  Subpackage for filters
              __init__.py
              equalizer.py
              vocoder.py
              karaoke.py
              ...
```

```
sound/effects/__init__.py
__all__ = ["echo", "surround", "reverse"]
# This would mean that from sound.effects import * would import the three named submodules of the sound package.
```

# Coding Styles
1. Pakai 4 spasi, no tab
2. Jangan lebih dari 79 karakter ke samping
3. dst

[Further Reading](https://www.python.org/dev/peps/pep-0008/)