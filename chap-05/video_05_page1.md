### Introduction Formats and Informats
* Informat tells sas how to read data and raw data. 
* It converts character value to numeric values.

* Format tells sas how to write a data.
*  To convert a numeric or character value into another character value.

sas defined formats:

```sas
proc print data =raw102.avderde;
var subject bodysys prefterm aestart;
foramt aestart date9.;
*format aestart mmddyy10.;
run;
```
* sas defined date  formats should be attached to a variable to re present in more meaningful way in output data set. 
But internal value of date variable is still in days. if we change in proc, it only attaches temporarily.
if we want to apply  format permanamtly to a variable, we need to do itin a data step. 

```sas
data adverse;
ser raw102.adverse;
format aestart mmddyy10.;
run;
```
sas defined informats:
Informat helpd sas to read data properly.

```sas
data dt:
input patno bthdt date9.; *informat
format bthdt mmddyy10.;
datalines;
100 1JAN1960
101 5JAN1960;
run;

##user defined formats and informats:

* to create a user defined informat, we use "invalue" statement. To apply that informat, we use "input" function. 
On the input function, we use informat.  That is going to convert a character value into numeric value.
* to do a numeric to character conversion, we need a format. A format is defined by using "value" statement.
The formats are used on a "put" function which will return the value based on what is stored in "order" variable and that will get stored in "parameter" variable.
* inforamt, invalue statement, input function use it together.
* foramt value statment put function use it together.
