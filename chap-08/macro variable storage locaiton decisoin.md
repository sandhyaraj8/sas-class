```sas
%let outname = t-demog;
%let output = &outname..rtf;

%macro report(outname=);
*Here will go the proc report and ods rtf statements;
 %letoutname = &outname..rtf;
 %put Inside report &outname;
 %mend;
 
 %macro rtf_out;
 %local output;
   %let output = %sysfunc(tranwrd (&outname,-,_));
   %put Inside rtf_out; Output =&output;
   %report (outname =&outname);
 %mend;
 
 %rtf_out;
 
 %put Outside rtf_out: Output =&output;
