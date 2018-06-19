### convert SAS7BDAT to XPT

```sas
libanme sasxpt xport "./xpt/ae.xpt";
proc copy in=sdtm102 out sasxpt;
select ae;
run;
 
 ### create macro and macro variable
 %macro xpt (dsname=);
 libanme sasxpt xport "./xpt/&dsname.xpt";
proc copy in=sdtm102 out sasxpt;
select &dsname;
run;

### to call macro in DM program

%xpt (dsname=dm);













data ae (sortedby =_null_);
set sdtm102.ae;
run;
