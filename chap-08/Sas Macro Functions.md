```sas
options nomprint nomlogic symbolgen;

data operation;
 sum ='+';
 multiply ='*';
 divide ='/';
 subtract='-';
 
 call symputx('operator' , sum);
 run;
 
 %macro arithmetic (variable1,variable2, operator);
  %let result = %eval(&variable1 &operator &variable2);
  &result;
  %mend;
  %put %arithmetic (1,2, &operator);
  
 /* %let result = %sysevalf(&variable1 &operator &variable2);
   %put %arithmetic (1.2,2.1, &operator); for decimal, we need %sysevalf functio n*/
   ```
  
