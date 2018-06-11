### Introduction Formats and Informats
* Informat tells sas how to read data and raw data. 
* It converts character value to numeric values.

* Format tells sas how to write a data.
*  To convert a numeric or character value into another character value.

sas defined formats:

```sas
proc print data =raw102.avderde;
var subject bodysys prefterm aestart;
format aestart date9.;
*format aestart mmddyy10.;
run;
```
* sas defined date  formats should be attached to a variable to re present in more meaningful way in output data set. 
But internal value of date variable is still in days. if we change in proc, it only attaches temporarily.
if we want to apply  format permanently to a variable, we need to do it in a data step. 

```sas
data adverse;
ser raw102.adverse;
format aestart mmddyy10.;
run;
```
sas defined informats:
Informat helps sas to read data properly.

```sas
data dt:
input patno bthdt date9.; *informat
format bthdt mmddyy10.;
datalines;
100 1JAN1960
101 5JAN1960;
run;
```

## user defined formats and informats:

* to create a user defined informat, we use "invalue" statement. To apply that informat, we use "input" function. 
On the input function, we use informat.  That is going to convert a character value into numeric value.
* to do a numeric to character conversion, we need a format. A format is defined by using "value" statement.
The formats are used on a "put" function which will return the value based on what is stored in "order" variable and that will get stored in "parameter" variable.
* inforamt, invalue statement, input function use it together.
* foramt, value statment, put function use it together.
 
 ### find out summary statistics of all patients who reported pain at month 3. 
 and re present summary statistics  show vertically not in default horizontally to show like the below.
  * n
  * Mean(STD) (concatenated)
  * Median
  * Min, Max (concatenated)


```sas
proc means data =raw102.pain nway;
var pain3mo;
output out =stats n=n mean=mean std=std min=mim max=max median =median;
run;
/*
*attach these values together and bring in this vertical form and transpose the DS.  take the data set and convert each statistcs into character.. bcoz character variable allows concatenate. 
* Use put fn and sas defined format 5.  -----. and strip function to take away extra spaces.
* use put fn and sas defined format 5.1 ----.- and strip function to take away extra spaces.
* use put fn and sas defined format 6.2 ----.--  and strip function to take away extra spaces.
* use || to concatenate
*/
data stats1;
ser stats;
nc= strip(put(n,5.));
meanstd = strip (put(mean,5.1)) ||"  ("||strip(put(std,6.2)) ||")";
medianc = strip(put(median,5.1));
minmax =strip(put(min,5.)) ||", " || strip (put(max,5.));
keep nc meanstd medianc minmax;
run;

proc transpose data = stats1 out =tstats1;
var nc meanstd meadianc minmax;
run;
proc format; /*new procedure*/
invalue stats /*create informat and name it as stats*/
"NC"=1
"meanstd" =2
"medianc" =3
"minmax" = 4;

value stats /* create format to tell sas to show/display stuff. u can use same name as "stats"*/
1= "N"
2 ="Mean (STD)"
3 = "Median"
4 = "Min, Max";
run;


/* define informat*/
data prefinal;
set tstats1;
order =input (_name_, stats.); /*order statement to keep the statistics in same order*/
parameter = put ( order,stats.); /* put fn helps us to apply a format to a variable and assign its value to another variable it this case from order variable, stats value gets captured in parameter variable*/
run;

title,footnote;
proc report data =prefinal nowd headline headskip split="|"; /* no sepearate window nowd, split the variable name using | */
column order parameter col1;
define order / order order=internal no print;
define parameter / display "statistics";
define col1 / display "Month 3|pain score";
run;


/*define informat*/
 

```
