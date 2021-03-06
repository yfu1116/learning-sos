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
![image](https://user-images.githubusercontent.com/44600656/60513250-52260280-9d09-11e9-9759-e774b0153bd6.png)

**4. about %run and 'variable' not defined**

- %run means SoS is executed independently and does not share any variables in the SoS kernel.
```
%run

[global]
excel_file = 'data/DEG.xlsx'
csv_file = 'DEG.csv'
figure_file = 'output.pdf'

[plot_10]
run: expand=True
    xlsx2csv {excel_file} > {csv_file}

[plot_20]
R: expand=True
    data <- read.csv('{csv_file}')
    pdf('{figure_file}')
    plot(data$log2FoldChange, data$stat)
    dev.off()
```

**5. & and executed in background**
![2](https://user-images.githubusercontent.com/44600656/60661122-d7d1bb80-9e8b-11e9-9e67-a27fbd282ebb.png)

**6. [workflow] Workflow cells cannot be executed directly**</br>
>if you execute the cell directly via Ctrl-Enter or Shift-Enter, it does not produce any output.</br>
```
[hello-world]
print('hello world')
```
**7. %sosrun**</br>
>**The %sosrun magic execute workflows defined in the embedded SoS script of a notebook.**</br>
>%sosrun hello-world</br>
>hello world</br>
>hello world again</br>
>**%run guideline https://vatlab.github.io/sos-docs/doc/user_guide/sos_in_notebook.html**</br>

**8. local and global variables**
>variables defined in individual steps are not available to other steps. </br>
>For example, the following workflow would fail.</br>
```
%run

[plot_10]
excel_file = 'data/DEG.xlsx'
csv_file = 'DEG.csv'

[plot_20]
figure_file = 'output.pdf'

R: expand=True
    data <- read.csv('{csv_file}')
    pdf('{figure_file}')
    plot(data$log2FoldChange, data$stat)
    dev.off()
NameError: name 'csv_file' is not defined
```
**9. %run --parameter</br>**
>https://vatlab.github.io/sos-docs/doc/user_guide/parameters.html</br>

**10. %expand**</br>
>![3](https://user-images.githubusercontent.com/44600656/60663736-a3adc900-9e92-11e9-85b5-39ad70368f39.png)</br>

**11. sep_output**</br>
```
%run -v0
[A]
output: 'a.txt'
_output.touch()

[B]
output: 'b.txt'
_output.touch()

[default]
input: output_from(['A', 'B'])
print(f'Input from step A is {_input["A"]}')
print(f'Input from step B is {_input["B"]}')
```
