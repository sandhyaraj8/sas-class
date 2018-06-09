## DataSet Programming
* To Manipute DataSet (aka Transformation) we use DataSet Programming
* We do not manipulate orginal (aka source) dataset
* we bring into work-library before creating new-DataSet. 
#### work-library 
* is TEMP library gets deleted at end-session
```bash
libname raw102 "~/AG102/data/raw";

data work.demog;
  set raw102.demographics; #it is going to read frm "set" and put in work.demog
run;  
```
* The "run;" marks as End
## Creating New Variable
