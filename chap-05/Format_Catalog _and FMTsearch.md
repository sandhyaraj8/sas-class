### Formats Catalog (saving permanemtly in catalogs)

* Formats and informats are stored in catalogs. Catalogs are stored in work library by default. 
* To save permanently by assigning lib= statement.
* SAS look first into work lib. need to tell sasto add lib in fmt search path.

```sas
option fmtsearch=(work fmt102);
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
```

### PROC Format CNTLIN/CNTL
* when we are given informat catalog and not its code, to make any changes


*To change the value of a format that already stored in a format catalog;
```sas
proc format lib=fmt102 cntlout=fmtout; /*cntlout option converts format into sas ds*/ 
select stats;
run;

data newfmt;
set fmtout;
if label = "Mean (STD)" then label ="Mean (SD)";
run;

*cntlin option converts a ds into a format;
proc format lib=fmt102 cntlin =newfmt;
run;

data test;
 text=put(2,stats.);
 run;
 
 proc print;
 run;
