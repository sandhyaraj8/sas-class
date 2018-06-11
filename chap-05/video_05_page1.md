### Introduction Formats and Informats
* Informat tells sas how to read data and raw data. 
* It converts character value to numeric values.

* Format tells sas how to write a data.
*  To convert a numeric or character value into another character value.

```sas
proc print data =raw102.avderde;
var subject bodysys prefterm aestart;
foramt aestart date9.;
*format aestart mmddyy10.;
run;
```
* sas defined date  formats should be attached to a variable to re present in more meaningful way in output data set. But internal value of date variable is still in days. if we change in proc, it only attaches temporarily.
if we want to apply  format permanamtly to a variable, we need to do itin a data step. 

```sas
data adverse;
ser raw102.adverse;
format aestart mmddyy10.;
run;
```
