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
