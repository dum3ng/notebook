The `__name__` variable is created when the script is imported or executed directly. If the script is executed directly, i.e. as the main process, `__name__` is assigned to "__main__" :

```bash
$ python myscript.py
```

If the script is imported as a module, then `__name__` is assigned as the module name:

```python
## file myscript.py
if __name__ == "__main__":
  pass
else:
  pass

## another file
import myscript

```

**Reason**:
The reason to create such a variable is you can write a module which can be both executed directly and imported, you would definitely not want to execute when just import it.