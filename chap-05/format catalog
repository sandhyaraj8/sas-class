### Formats Catalog (saving permanemtly in catalogs)

* Formats and informats are stored in catalogs. Catalogs are stored in work library by default. 
* To save permanently by assigning lib= statement.
* SAS look first into work lib. need to tell sasto add lib in fmt search path.

```sas
option fmtsearch=(wor fmt102);
proc format lib =fmt102;
invalue stats
  NC" = 1
 "MEANSTD" = 2
 "MEDIANC" = 3
 "MINMAX" =  4;

 value stats
 1 = "N"
 2 ="Mean (STD)"
 3 = "Median"
 4 = "Min, Max";
run;
```sas
