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
```
2.4.3. Formatted string literals
New in version 3.6.

A formatted string literal or f-string is a string literal that is prefixed with 'f' or 'F'. These strings may contain replacement fields, which are expressions delimited by curly braces {}. While other string literals always have a constant value, formatted strings are really expressions evaluated at run time.

Escape sequences are decoded like in ordinary string literals (except when a literal is also marked as a raw string). After decoding, the grammar for the contents of the string is:

f_string          ::=  (literal_char | "{{" | "}}" | replacement_field)*
replacement_field ::=  "{" f_expression ["!" conversion] [":" format_spec] "}"
f_expression      ::=  (conditional_expression | "*" or_expr)
                         ("," conditional_expression | "," "*" or_expr)* [","]
                       | yield_expression
conversion        ::=  "s" | "r" | "a"
format_spec       ::=  (literal_char | NULL | replacement_field)*
literal_char      ::=  <any code point except "{", "}" or NULL>
```

