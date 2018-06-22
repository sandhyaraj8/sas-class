```sas
%let p=proc print data =DSN; run;;
%put &p;

/*during compile time use %str function to mask ; to treat it as part of the text*/
 
 %let p=%str (proc print data=DSN; Run;);
 %put &p;

%let Company = J&J;
%put &company;

/* use %nrstr to mask  & in J&J to treat it as a text instead of macro symbol*/

%let Company = %nrstr(J&J);
%put &company;

%macro client1; *error...???;

/* first resolve the &name, after compilation, during run time use 
%bquote function to mask "/" in Anova/Gaddu*/
 
 data client;
name'Anova/Gaddu';
call symputx('name', name);
run;

%if %bquote(&name) eq %str ( )  %then %do;
%put "Error: Required parameter is blank";
%goto exit;
%end;

%put Client Name is : &name;

%exit:
%mend;
%client1;

/*another runtime masking function*/
%macro client2;
data client;
 name = 'Anova&Gaddu';
 call symputx('name' , name);
 run;
 
 %let name =%nrbquote (&name); *we get a warning with this function;
 
 %if &name eq %str( ) %then %do;
  %put "Error: Required parameter is blank";
  %goto exit;
 %end;
 
 %put client name is: &name;
 %exit:
 %mend;
 %client2;
 
 %macro client3; * again no results...???;
 
 data client;
 name = 'Anova&Gaddu';
 call symputx('name', name);
 run;
 *%superq function tries to mask & in Anova&Gaddu without resolving it;
 %let name =%superq (name); *no & and we don't get warning msg when we run;
 
 %if &name eq %str( ) %then %do;
  %put "Error: Required parameter is blank";
  %goto exit;
 %end;
 
 %put client name is: &name;
 %exit:
 %mend;
 %client3;
 
 ```
