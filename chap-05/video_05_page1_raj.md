* Informat tells Sas How to read RAW data
* Format tells SAS How to Write (display and print reports)

## Sas Defined Formats
* we will see, how to create own format+Informats
* In raw102.adverse, notice aestart is in int-type like 18357 is that many day ssince 01Jan1960
* as soon as we apply format as "format aestart date9.;" shows as 05APR2010
* This ishow we attach format to a variable.
* data9. is sas defined (meaning Standard,) another example is mmddyy10.; so output = 05/04/2010

* Notice: the format keyword inside "proc print"
```sas
proc print data=raw102.adverse;
var subject aestart;
format aestart mmddyy10.
run;
```

* NOTICE: format is attached temporarily (only inside proc-print scope
* But to apply "format" permemanetly we need to do inside DATA-step
```sas
data adverse;
set raw102.adverse;
format aestart mmddyy10.;
run;
```
* ! in above example format is PERMananently applied for aestart in that data-set

