#EC Toolkit Tables#

##List of Tables##

###Primary Tables###
The below tables are primary tables. These are primarily replicas of the original SIS tables, but, for de-normalized.  The data into these tables are populated by "Synchronization" process.

|Category |Table Name | Purpose|
|---------|-----------|--------|
|Period Related |ELECTIVE_PERIOD | This table denotes the period of EC Allocation. During this period students are eligible to select/add/drop course (sections) of their choice. Theoretically, There can be only one elective period per EC phase. It is configured in SIS through TKMS activity task.|
|Period Related |ALLOCATION_PERIOD | This table captures the various allocation periods available. Allocation periods denote the various phases with in the Elective Period. e.g. Pre-registration Entry, Pre-registration Follow Up, Fall Add-Drop, Spring Add Drop, Jan Add Drop. These are the periods defined by PRMS and ADMS activity tasks. |
|Activities |PROGRAM_SESSION | This table captures all the program sessions in SIS.|
|Activities |EC_PHASE | This table captures all the phases. This table includes program session id.|
|Activities |TERM | This table captures all the terms in SIS. This includes phase, program session id and program id|
|Activities |COURSE | This table captures all the courses in SIS. It includes term, phase program session and program ids |
|Activities |COURSE_SECTION | This table captures all the courses sections in SIS. It includes course id, program session id and term id |
|Person Info |PERSON | This table captures all the person information. It contains the details about every one in the system i.e., Student Staff and Faculty|
|Course Unit |UNIT | This table captures all the units available in SIS.|
