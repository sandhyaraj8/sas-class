## DataSet Programming
* To Manipute DataSet (aka Transformation) we use DataSet Programming
* We do not manipulate orginal (aka source) dataset
* we bring into work-library before creating new-DataSet. 

### Keep/Drop statement allows to keep/drop Vars in output-dataset

#### work-library 
* is TEMP library gets deleted at end-session
* it is going to read frm "set" and put in work.demog
```bash
libname raw102 "~/AG102/data/raw";

data work.demog;
  set raw102.demographic; 
run;  
```
* The "run;" marks as End
## Creating New Variable
* example : trtc = Placebo when trt=0 or Active when trt=1
```bash
libname raw102 "~/AG102/data/raw";

data work.demog;
  set raw102.demographic; 
  
  if trt=0 then trtc = "Placebo";
  else if trt=1 then trtc = "Active";
  else PUT "Warning: TRT variable has different value=" trt= ;
run;  
```

## Keeping variables
```bash
libname raw102 "~/AG102/data/raw";

data work.demog;
  set raw102.demographic; 
  
  if trt=0 then trtc = "Placebo";
  else if trt=1 then trtc = "Active";
  else PUT "Warning: TRT variable has different value=" trt= ;
  
  KEEP uniqueid trt trtc
run;  
```

## DROP Variables
* It drops those variables ONLY in output dataset

```bash
libname raw102 "~/AG102/data/raw";

data work.demog;
  set raw102.demographic; 
  
  if trt=0 then trtc = "Placebo";
  else if trt=1 then trtc = "Active";
  else PUT "Warning: TRT variable has different value=" trt= ;
  
  DROP uniqueid dob randdt
run; 
```
