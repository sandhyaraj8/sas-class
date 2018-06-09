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
##### LABS has LabTest data
* Each Subjectid will have LabTest+LabCategory Names, and test units along with Range (ie., LOW/HIGH) along with LABdate (when it was run)
