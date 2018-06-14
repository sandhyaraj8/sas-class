## Creating Runtime format
* When input dataset is in CODED-format
* example testc0des of 1,2,3 maps to another lookup as HGB,HGB,BILI

```sas
data lab;
input subject testcd result;
datalines;
100 1 90
100 2 80
100 3 70
;
run;

proc import file="~/exercise/lab.xlsx"
dbms=xlsx out=ct replace;
run;

/* written statically */

proc format;
value testfmt
1="HGB"
2 = "PLAT"
3="BILI"
;
run;

/* create dataset in specific variables-format */

data fmtin;
   set ct;
   
   start=coded;
   end=coded;
   fmtname = "testfmt";
   label=decoded;
   type="N";
run;

data lab1;
  set lab;
  lbtestcd=put(testcd, testfmt.);
run;

proc print;
run;

```
