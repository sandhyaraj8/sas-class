## PROC Step processing

* PROC - Procedures are the functions which use the prepared DataSets (using DATA stmt) to produce/print analysis/result/reports.
* example: Note: noobs-removes Obs seqid column from results, label keyword in print says, label names are same as variable names

#### PROC Print
```bash
libname raw102 "~/AG102/data/raw";

proc
    print data=raw102.demographic noobs label;    
    var subject trt dob;
    where trt=1;
    
    label subject = "Subject Indentifier";
run;
```

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
* To calculate Mean
* Notice 01Jan1960 is Day 0 in Sas Date Object, whihcis equivalent to 0 int value


