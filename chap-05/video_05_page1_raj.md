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
* notice strip removes leading-spaces example 5.2 of "59" data there wil be "3spaces+59.xx" so strip fn (actually trims it)
* Notice how mean value of 1.8309etc., gets rendered as 1.8 only !! because of 5.1
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
* we will transponse to make starts names to columns

```sas
proc transponse dta=stats out=tstats;
var nc meanstd meadinc minmax;
run;
```
* we will create our own format now caled "stats." (also called User defined format!)
```sas
proc format;
invalue stats
"nc"=1
"meanstd"=2
"medianc"=3
"minmax"=4
;
run;
```

* now we are applying above UD-format

```sas
data prefinal;
set tstats1;
order = input(_name_, stats.);
parameter = input(order, stats.);
run;
```

* written above to add new format-for-display

```sas
proc format;
invalue stats
"nc"=1
"meanstd"=2
"medianc"=3
"minmax"=4
;

value stats
1="N"
2="Mean (STD)"
3="Median"
4="Min,Max"
;
run;
```

* we wil use "report" to render a report

```sas
proc report dta=prefinal nowd headline headskip split="|";
column order parameter col1;
define order / order order=internal noprint;
define parameter /display "statistics";
define col1 / display "Month 3| Pain Score";
run;
```

* Baically we create informat using "invalue" to apply this informat to variable=name we use input(_name, stats.)
* to create            format using "value" stmt to apply this format on some-data we use put and assign to parameter variable


```
