### convert SAS7BDAT to XPT

```sas
libanme sasxpt xport "./xpt/ae.xpt";
proc copy in=sdtm102 out sasxpt;
select ae;
run;
 
* create macro and macro variable;
 %macro xpt (dsname=);
 libanme sasxpt xport "./xpt/&dsname.xpt";
proc copy in=sdtm102 out sasxpt;
select &dsname;
run;

* to call macro in DM program;

%xpt (dsname=dm);

/* sortedby is a flag tells if input ds is sorted or not.This metadata 
cannot be passed to XPT file, so it has to be nulled out first*/

data ae (sortedby =_null_);
set sdtm102.ae;
run;
*instead of typing same code except ds name, we can create macro;

libname sasxpt xport "~/AG102/data/sdtmxpt/ae.xpt";
proc copy in=work out=sasxpt;
select ae;
run;

libname sasxpt xport "~/AG102/data/sdtmxpt/dm.xpt";
proc copy in=work out=sasxpt;
select dm;
run;

%macro create_xpt (dsname=);
libname sasxpt xport "~/AG102/data/sdtmxpt/&dsname..xpt"; /* we need 2 dots in order to get dsname properly with .xpt, unless there is space in b/w .xpt*/
proc copy in=work out=sasxpt;
select &dsname;
run;
%mend;

*calling macro for folloeing ds;
%create_xpt(dsname=dm);
%create_xpt(dsname=ae);
%create_xpt(dsname=xp);

libname sasxpt xport "~/AG102/data/sdtmxpt/ae.xpt";

proc copy in=work out=sasxpt;
select dm;
run;
```


