## Format Catalog
* User defined Fomats+Informats are stored in "catalogs" and catalogs are stored in work-library having session life scope
* Notice below, how change in first line with lib= puts infomat+format into fmt102-catalog and not int owork catalog

```sas
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
