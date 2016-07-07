#EC Toolkit Tables#

##List of Tables##
|Category |Table Name | Purpose|
|---------|-----------|--------|
|Period Related |ELECTIVE_PERIOD | This table denotes the period of EC Allocation. During this period students are eligible to select/add/drop course (sections) of their choice. Theoretically, There can be only one elective period per EC phase. It is configured in SIS through TKMS activity task.|
|Period Related |ALLOCATION_PERIOD | This table captures the various allocation periods available. Allocation periods denote the various phases with in the Elective Period. e.g. Pre-registration Entry, Pre-registration Follow Up, Fall Add-Drop, Spring Add Drop, Jan Add Drop. These are the periods defined by PRMS and ADMS activity tasks. |
|Activities |PROGRAM_SESSION | This table captures all the program sessions in SIS.|
|Activities |TERM | This table captures all the terms in SIS. This includes phase, program session id and program id|
|Activities |Course | This table captures all the courses in SIS. It includes term, phase program session and program ids |
|Activities |Course | This table captures all the courses sections in SIS. It includes course id, program session id and term id |