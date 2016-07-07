#EC Toolkit Tables#

##List of Tables##

|Category |Table Name | Purpose|
|---------|-----------|--------|
|Period Related |ELECTIVE_PERIOD | This table denotes the period of EC Allocation. During this period students are eligible to select/add/drop course (sections) of their choice. Theoretically, There can be only one elective period per EC phase. It is configured in SIS through TKMS activity task.|
|Period Related |ALLOCATION_PERIOD | This table captures the various allocation periods available. Allocation periods denote the various phases with in the Elective Period. e.g. Pre-registration Entry, Pre-registration Follow Up, Fall Add-Drop, Spring Add Drop, Jan Add Drop. These are the periods defined by PRMS and ADMS activity tasks. |
|Activity |PROGRAM_SESSION | This table captures all the program sessions in SIS.|
|Activity |EC_PHASE | This table captures all the phases. This table includes program session id. This table has aggregated EC phase related data stored in JSON format. The JSON data includes data such as courses and students.|
|Activity |TERM | This table captures all the terms in SIS. This includes phase, program session id and program id|
|Activity |COURSE | This table captures all the courses in SIS. It includes term, phase program session and program ids |
|Activity |COURSE_SECTION | This table captures all the courses sections in SIS. It includes course id, program session id and term id |
|Person Info |PERSON | This table captures all the person information. It contains the details about every one in the system i.e., Student Staff and Faculty|
|Course |UNIT | This table captures all the units available in SIS.|
|Course |COURSE_UNIT | This is a mapping table between course and unit |
|Course |COURSE_PREREQUISITE | This table contains the pre-requisite courses for any given course.|
|Course |MUTUALLY_EXCLUSIVE_COURSE | This table contains the mutually exclusive courses for any given course|
|Course Section |LESSON_EVENT | This table contains all the lessons and meeting template details of a course section|
|Course Section |COURSE_SECTION_FACULTY | This table contains the faculty details of a given course section.|

