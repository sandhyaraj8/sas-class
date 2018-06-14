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

## SAS defined INFormats
* meaning to read properly, example below
* we have data as below, where we notice data is liek open string [1Jan1960]
```sas
data dt;
input pat_num bth_dt date9.;
*format bth_dt mmddyy10. used to render/display only
datalines;
100 01Jan1960
101 05Jan1960
;
run;
```

## User defined Formats and Informats
* say want to create stats for pain3mo in pain DS
* the belo  snippet shows stats horizontally
```sas
proc print data=raw102.pain nway;
  var pain3mo;
  output out=stats n=n mean=mean std=std min=min max=max median=median;
run;
```

* but if we want vertically and 2 vriables concatenated as
* So we are going to convert all display data into CHARacter data, by using put-function
```sas
/*
N
Mean(STD)
Median
Min, Max
*/

data stats1;
  set stats;
  nc = strip( put(n,5.) );
  meanstd = strip( put(mean,5.) )  || "(" || strip( put(std,6.2) ) || ")";
  
  keep nc meanstd;
run;
```
