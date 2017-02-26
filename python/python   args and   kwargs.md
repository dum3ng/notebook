### used in function defination
`*args` can allow one to enter any number parameters, they are wrapped in an array:

```python
def hello(name, day='today', *args):
  return 'hello {name}, {day}, {a},{b}'.format(name=name, day=day, a=args[0], b=args[1])
# now call
hello('kael','this day', 3, 4)

```

`**kwargs` can allow one to enter any optional number key-value parameter.
The `*args* must come before `**kwargs`, a mixed example:
```python
def foo(a, *args, **kwargs):
  pass

# now call it
foo(3, 4, 5, operation='add', out='std')
```

---
### used as unpack operator
The `*` and `**` can be used as unpack operator in function call:
```python
# * can unpack an array
def foo(a, b, c):
  pass

d = [1, 2, 3]
foo(*d)

# and ** can unpack a dictionary
def bar(**kwargs):
  pass

m = {'a':3, 'b':4'}
bar(**m)

# this can be useful in string format
data={'name':'jim', 'place':'china'}
'{name}, you are in {place}'.format(**data)
```
Note that this does not work in normal expression.

---
###

