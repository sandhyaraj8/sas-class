## Selecting Observations - aka. Filtering Rows
* note Difference at "IF Gender" and "If Then" They serve DIFFERENT purpose
* Here only male rows are selected into output dataset (aka Filtering)

```bash
data work.demog;
  set raw102.demographic; 
  
  IF gender = 1;
  
  if trt=0 then trtc = "Placebo";
  else if trt=1 then trtc = "Active";
  else PUT "Warning: TRT variable has different value=" trt= ;
  
  DROP uniqueid dob randdt
run; 
```

## Limiting input-variable by keep and drop OPTIONS
* Note the "keep=" statement is put insame line of "set", this reads ONLY those variables from input-dataset
```bash
data work.demog;
  set raw102.demographic  (keep= uniqueid trt) ; 
  
  if trt=0 then trtc = "Placebo";
  else if trt=1 then trtc = "Active";
  else PUT "Warning: TRT variable has different value=" trt= ;
run;
```

![PDV Image](Capture_PDV_chap02_a.PNG)

## Compilation & Execution Phase
* During Compilation 3 things happen
  * check syntax, (trtc is derived variable)
  * create PDV (PDV holds one row in memory, as sas processes one row at a time)
  * Create output Metadata (variable label, type, name, format/informat etc.,)
 * During Execution Phase
  * takes one obs to PDV
  * "_N_" = 1, for first row (index)
  * "_ERROR_" will be 0 or 1 based on input error or not

## IF vs WHERE (output statement)
```bash
libname raw102 "~/AG102/data/raw";

data work.male work.female;
  set raw102.demographic; 
  
  if gender=1 then output work.male;
  if gender=2 then output work.female;
run; 
```

* "if" is changed to "where"
* "IF" is applied on PDV, "where" is NOT
" Where is more-effecient than IF because it reads from input-buffer, before going to PDV

## Statement vs Option
```bash
libname raw102 "~/AG102/data/raw";

data 
  work.male (keep= subject trt dob) 
  work.female (keep= subject trt randdt);
  set raw102.demographic; 
  
  if gender=1 then output work.male;
  if gender=2 then output work.female;
run; 
```
