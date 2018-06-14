## Format Catalog
* User defined Fomats+Informats are stored in "catalogs" and catalogs are stored in work-library having session life scope
* Notice below, how change in first line with lib= puts infomat+format into fmt102-catalog and not int owork catalog
* the options header lines says the serac horder in lib names

```sas
options fmtsearch=(work fmt102);

*proc format;
proc format lib=fmt102;
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

* as utility you can LIST all catalogs inside-an-catalog too using
```sas
proc format lib=fmt102 fmtlib;
run;
```

* If we are already given a catalog as below without source code
```sas
proc format lib=fmt102 fmtlib;
select stats;
run;
```
* Notice above gives output as start, end, label as
* 1,1,N
* 2,2, Mean(STD) {And our aim is to change this to Mean(SD) }
* To change lke above we play into dataset

### Here we are going to OverWrite a catalog defined Label !

```sas
proc format lib=fmt102 fmtlib cntlout=fmtout;
select stats;
run;
```
* see above output, notice line 2 =  now changeing STD to SD
```sas
data newfmt;
 set fmtout;
 if label = "Mean (STD)" then label = "Mean (SD)";
run;
```

* As test program

```sas
data test;
 text=put(2, stats.);
run;

proc print;
run;
```
