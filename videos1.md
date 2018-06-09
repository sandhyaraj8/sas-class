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
