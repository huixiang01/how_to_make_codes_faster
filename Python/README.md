<h1>How to make python code run faster</h1>

Simple guide to become a potential successful hackathon winner

<h2> 1. Know the basic structure</h2>

Structure can affect your codes very drastically. Are you dealing with dictionary, hashes, array or set?  What objective you want to achieve? These questions are the some of the many few questions you must ask yourself about. So, yup! Let's get things right

<h3>For List</h3>

|                        **Operation**                         | **Average Case** | Amortized Worst Case |
| :----------------------------------------------------------: | :--------------: | :------------------: |
|                             Copy                             |       O(n)       |         O(n)         |
|                          Append[1]                           |       O(1)       |         O(1)         |
|                           Pop last                           |       O(1)       |         O(1)         |
|                       Pop intermediate                       |       O(k)       |         O(k)         |
|                            Insert                            |       O(n)       |         O(n)         |
|                           Get Item                           |       O(1)       |         O(1)         |
|                           Set Item                           |       O(1)       |         O(1)         |
|                          Iteration                           |       O(n)       |         O(n)         |
|                          Get Slice                           |       O(k)       |         O(k)         |
|                          Del Slice                           |       O(n)       |         O(n)         |
|                          Set Slice                           |      O(k+n)      |        O(k+n)        |
|                          Extend[1]                           |       O(k)       |         O(k)         |
| [Sort](http://svn.python.org/projects/python/trunk/Objects/listsort.txt) |    O(n log n)    |      O(n log n)      |
|                           Multiply                           |      O(nk)       |        O(nk)         |
|                            x in s                            |       O(n)       |                      |
|                        min(s), max(s)                        |       O(n)       |                      |
|                          Get Length                          |       O(1)       |         O(1)         |



<h3> Exceptions</h3>

|             Types              | **Operation** | **Average Case** | **Amortized Worst Case** |
| :----------------------------: | :-----------: | :--------------: | :----------------------: |
| Dictionary/Collections vs List |  Delete Item  |   O(1) vs O(n)   |           O(n)           |

# Set

| **Operation**                     | **Average case**                                             | **Worst Case**                                | **Notes**                                  |      |      |
| :-------------------------------- | :----------------------------------------------------------- | :-------------------------------------------- | ------------------------------------------ | ---- | ---- |
| x in s                            | O(1)                                                         | O(n)                                          |                                            |      |      |
| Union s\|t                        | [O(len(s)+len(t))](https://wiki.python.org/moin/TimeComplexity_(SetCode)) |                                               |                                            |      |      |
| Intersection s&t                  | O(min(len(s), len(t))                                        | O(len(s) * len(t))                            | replace "min" with "max" if t is not a set |      |      |
| Multiple intersection s1&s2&..&sn |                                                              | (n-1)*O(l) where l is max(len(s1),..,len(sn)) |                                            |      |      |
| Difference s-t                    | O(len(s))                                                    |                                               |                                            |      |      |
| s.difference_update(t)            | O(len(t))                                                    |                                               |                                            |      |      |
| Symmetric Difference s^t          | O(len(s))                                                    | O(len(s) * len(t))                            |                                            |      |      |
| s.symmetric_difference_update(t)  | O(len(t))                                                    | O(len(t) * len(s))                            |                                            |      |      |



<h2>2. Reduce Memory Footprint</h2>

Instead of incrementing the input, it is better to do it in one-shot. Like the following:

```python
# instead of this:
msg = input()
msg += input()
msg += input()

# Do this:
msg = [input(), input(), input()]
# it would be better to write a code if the user has given no. of input rows
```

Formatting of string:

```python
# slow
SUTD = "hello" + people + "world"

# faster
SUTD = " hello %s world" % people

#faster-est
SUTD = "hello {} world".format(people)

```

Sorting:

```python
# slow : this makes a copy. Good if you need a copy, but most likely you don't
s = sorted(list)

# faster :  No copyb required
list.sort()

```

If conditions:

```python
# Minimise checking  true = true:
if condition: function()

# rather than this:
if condition == true: fucntion()
    
```

<h2> 3. Use Built-in functions</h2>

They are there for a reason: to optimize to the max! They are built in C by the way...

Mapping:

```python
newList = []
for word in oldList:
    new.list.append(word.upper())
# for loop is very annoying. Because of this, there can be a better in doing stuff.

newList = map(str.upper, oldList) 
```

If you wanna find out why map() can be faster than for loop, you might to try with a smaller sample. For more information, find out [here](https://medium.com/@ExplosionPills/map-vs-for-loop-2b4ce659fb03)!

Collections:

```python
s = [('yellow', 1), ('blue', 2), ('yellow', 3), ('blue', 4), ('red', 1)]
d = defaultdict(list)
for k, v in s:
    d[k].append(v)
    
# And this:
Counter('mississippi')
>>> Counter({'i': 4, 's': 4, 'p': 2, 'm': 1})
```



<h2>
    4. Loops
</h2>

Why not use regex cache instead?

```python
# Instead of this:
for i in big_it:
    m = re.search(r"\s-\s", input())
    if m:
        function()
        
# do this: compile this and use cache
date_regex = re.compile(r"\s-\s")

for i in big_it:
    m = date_regex.search(i)
    if m:
        function()
```

If you can't use, why not use local and global variables? i am sure if you know python, you should know how to use ^_^.

If you got a class and its method, use it please!

```python
myfunc = myObj.func
fcor i in range(n):
    myfunc(i) # faster than myObj.func(i)
```

<h2> 5. Keep Your Code Base Small


</h2>

How? 

1. When you import a module, use functions that only serve the intended purpose. Don't make unnecessary computations!
2. Reduce the no. of conditional statements in the code



<h2>    Final Question: How to Spot Performance Issues???</h2>

Use this command !

```python
python -m cProfile [-o output_file] [-s sort_order] myscript.py

```

