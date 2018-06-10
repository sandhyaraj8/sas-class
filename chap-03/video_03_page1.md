## PROC Step processing

* PROC - Procedures are the functions which use the prepared DataSets (using DATA stmt) to produce/print analysis/result/reports.
* example: Note: noobs-removes Obs seqid column from results, label keyword in print says, label names are same as variable names

#### PROC Print

libname raw102 "~/AG102/data/raw";

proc
    print data=raw102.demographic noobs label;    
    var subject trt dob;
    where trt=1;
    
    label subject = "Subject Indentifier";
run;

#### PROC Sort
```bash
libname raw102 "~/AG102/data/raw";

proc sort 
    data=raw102.demographic 
    out=work.demog1 (keep= subject trt);    
    by descending trt;
run;

proc sort 
    data=raw102.demographic 
    out=work.demog1 (keep= orace) nodupkey;    
by orace;
run;
```

#### PROC Freq
* Say we want to see frequency (ie count) by another variable
* How many patients are Placebo or Active
* Notice cross-tabulation using * and it generates the freuqency output to a `new dataset `

```bash
libname raw102 "~/AG102/data/raw";

data demog;
    set raw102.demographic;
    keep subject trt gender;
run;

proc freq data= demog;
    table trt * gender / out= freq;
run;
```
#### PROC Means
* To calculate Mean, on a continuous-variable
* Notice 01Jan1960 is Day 0 in Sas Date Object, which is equivalent to 0 int value
* Notice: in format line below only variable name is specified, but format pattern is missing, that makes sas to apply best-for-numeric
    * so the randdt, dob are displayed as int-values and not as mm/dd/yyyy display format earlier (by default)
* notice in metadata type in results-tab the format value is "empty" before that it shows "MMDDYY10" as format

* nway removes the total classification type from proc output DS
* class (categorial variable) trt gives measn group-by trt ie., 0 and 1
* output is the one taking the proc result to ds name

```bash
libname raw102 "~/AG102/data/raw";

data dt;
    dt1='01Jan1960'd;   
run;

data demog;
    set raw102.demographic;
    age = (randdt - dob)/365.25;
    keep subject trt age randdt dob;
    
    format randdt;
    format dob;
run;

proc means data= demog nway;
    var age;
    class trt;
    output out=stats;
    
run;
```
