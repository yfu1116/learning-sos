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

