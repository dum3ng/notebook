1. Alwasy use absolute import.
2. Use dot `.` to explicitly use relative import.

When using absolute import for current package, you can not run the script directly, that will cause an import error. 
Use module switch instead:

```bash
;;error
$ python mod0.py  

;; use module switch
$ python -m pack.mod0
```

Relative import:
```python
## in A.B.C module
import .mod0  ## A.B.mod0
from . import mod1  ## A.B.mod1
from .. import mod2 ## A.mod2
```

---
~Deprecated~:
### import from same directory
If one file is the root path,
#### import a file from another file

File structure is:
```
folder/
  a.py
  b.py
```
Then you can use:
```python
## in b.py
import a
```
#### import a file in another directory
File structure is :
```
folder/
  a.py
b.py
```
You can add a `__init__.py` to folder to make it as a package, then import it:
```python
## after change
'''
folder/
  __init__.py
  a.py
b.py
'''
## in b.py
from folder import a
```

### import from different directory
If both the imported file and current file are in different folders, then the file structure should be:
```
packs/
  __init__.py
  pack0/
    __init__.py
    a.py
  pack1/
    b.py
```
The parent folder should also be a package, then use:
```python
# in b.py
from packs.pack0 import a
```

**warning:**
You can not use the package name at package root:
```
packs/
  __init__.py
  pack0/
    __init__.py
    a.py
  core.py
```
If one want to use functions in a.py, then `from packs.pack0 import a` will cause an error: ` packs is not a package`.

In this situation, just use `from pack0 import a`, because it is in the root path.

---