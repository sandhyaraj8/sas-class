```sas

*Macro Variable;
*Automatic Macro variable;
%put _automatic_;
%put &sysdate;

*user defined variables;
*delayed resolution use 2 ampersand resolve to 1 ampersand;
    %let car =Honda;
    %let honda =economy;
    %let economy =30-50k;

    %put &car is a &honda  car priced between economy;
    %put &car is a &&&car car priced between &&&&&&&car;

/*
 &&&car
       &Honda
        economy
 &&&&&&&car
       &&&Honda
         &economy
            30-40k
   */
*what happens when macro variable car changes;
    %let car =BMW;
    %let BMW = Hignend;
    %let Highend = 50 - 100k;

    %put &car is a &honda  car priced between economy;
    
    %put &car is a &&&car car priced between &&&&&&&car;
    
 /*
   &&&car
      &BMW
          highend
   &&&&&&&car
        &&&BMW
         &highend
          50-100
   */
  */
  ```
