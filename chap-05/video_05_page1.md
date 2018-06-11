### Introduction Formats and Informats
* Informat tells sas how to read data and raw data. 
* It converts character value to numeric values.

* Format tells sas how to write a data.
*  To convert a numeric or character value into another character value.

```sas
proc print data =raw102.avderde;
var subject bodysys prefterm aestart;
run;
```
