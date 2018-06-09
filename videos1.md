* Get Access  https://odamid.oda.sas.com Sas OnDemand for Academics (or Sas Studio) for Registration to get online acess to class+data
* LIBnAME or FILENAME is used to load course sample data

### Sas Studio
* `My Folders` will be root for all data and programs
#### Create Folder and Load data
* The below steps will guide to get data created from `my_courses/anovagroups/Sample_AG102` to `My Folders/AG102`
* my_courses/anovagroups/Sample_AG102 it has folders "macro,metadata,programs,rawdata,setup"
* inside setup/*.sas run 6 sas files (they are sas programs), we notice `My Folders/AG102` is created and data files under them
#### Understanding Sas DataSet
* Columns = Variables (can be 3) Numeric,Character and Special (for Date etc.,)
* Rows = Observations
* Notice MetaData about a DataSet rendered (like column details)
#### Sas Ent Guide
* To download standalone studio (works only on Windows) it uses acount to connect to sas-cloud
* You  can create new sas program
* Expand "SasApp" whihc opens same cloud app files
* To run a sas program, say ~/AG102/prog/adtm/dm.SAS, run as run or Run-selection
* Notice below  `statusbar` it shows cloud connected and current status of programs execution status
#### Creating SDTM and ADAM datasets
* From SEGuide navigate to Servers /AG102/programs/sdtm/dm.sas
* goto output dir to see data of dm.sas into /AG102/data/sdtm/dm.sas
* repeat ae,ds,ex,lb,tdm,xp.sas into /AG102/data/sdtm/* (ignore alert pop-up, ok) - notice for "error/warning/notes" window
* repeat for "adam", into /AG102/data/sdtm/* 
* adsl.sas should be FIRST in adam and come to adam only after sdtm!
#### Creating Library
* Our raw data is  in AG102/data/raw
* ! to view/render raw data in studio, we should create a "link" uisng LIBNAME stmt
* example LIBNAME raw102 "/home/blah/data/raw" creates logical name and execute
* Navigate to "Libraries" in studio you see a NODe called "RAW102"
* ! Folder is physical location, Libraries is logical connection 
#### PROC Print and Contents

* to view RAW-data content in "results" tab, execute 
```bash
libname raw102 "/blah/data/raw"

proc print data = raw102.demographic;
run;
```
* to view METADATA-data content in "results" tab, execute (diff is "contents" instead of "print")
```bash
libname raw102 "/blah/data/raw"

proc contents data = raw102.demographic;
run;
```
* It gives VERY detailed info like data-types, count of abs and variables, sorted etc.,

#### Understanding Raw Data
* To look at rawdata, we need to create library, instead we run init.sas, this creates Libraries
* We are interested in "RAW102" library (after refresh in Navigate bar)
##### Adverse Data
* When we read though "Adverse" raw data , we notice for subjectid = 101 and 301 there are couple of observations
* PREFTERM is generic "adverse effect name" describes what adverse effect it was, and AEStart and AEEnd dates
* BODYSYS tells about whihc "system organ class" example "convulsion" is coming from "Nervous system disorder"
* AEREL tells to the "level" ( 1 to 3) of how effectivly it is releated to the "trial" clinical drug it was!!
* (hold ur mouse on AEREL header) you notice possible values which are called LABELs (it is metadata to a variable)
* AESEV is severity, AEREACTION says about action taken
* NOTICE, AEStart and AEEnd dates are in SAS Date Format - Ho wmany days since 01/01/1960 (it is like int), but we need to put format to display real date
* NOTICE ther are dupe rows for subjectid, because each person can have many observations
##### Demographics data
* NOTICE ther are SINGLE row for subjectid, it has subject/pateint demographics details
* TRT says 0/1 mean pil was not taken (liek placebo drug) 1 means he was given test-drug
* RANDDT is the date when TRT wa assigned/applied for Subjects
##### Dosing data
* Each Subject will have start+end date and DailyDose count, notice it has other normalized columns like mm, dd, year for start+end
