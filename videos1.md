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

* to view raw data content, execute 
```bash
libname raw102 "/blah/data/raw"

proc print data = raw102.demographic;
run;
```
