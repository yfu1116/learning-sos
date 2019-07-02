# Notes of SoS
1. SoS automatically shares variables with names starting with sos among all subkernels.

2. variables defined in individual steps are not available to other steps. 

3. Special format specification for _input objects
```
SoS variables _input and _output are of type sos_targets and accept additional format specifications. For example,
:n is the name of the path. e.g. f'{_input:n}' returns /path/to/a if _input is /path/to/a.txt
:b is the basename of the path. e.g. a.txt from /path/to/a.txt
:d is the directory name of the path. e.g. /path/to from /path/to/a.txt
```
![avatar](‪C:\Users\dell\Desktop\草图.png)
