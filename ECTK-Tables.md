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
|Course Section |ELECTIVE_COURSE_SECTION | This table contains the mapping between course sections and elective periods|
|Person |ELECTIVE_PERIOD_STUDENT | This table contains the mapping between elective period and students. This gets the student from the ACADEMIC_PHASE_ENROLLMENT table |
|Person |EXCLUSION_SET | A student may want to exclude courses from is view on the schedule view. This table holds the master details about the exclusion set. |
|Person |EXCLUSION_SET_COURSES | This table contains the mapping between exclusion sets and courses |
|Person |STUDENT_REQUESTS | This table contains the requests created by the student. All the requests are stored in a single column as a JSON. |
|Person |STUDENT_PRIORITIZATION | The table contains the special course allocation requests created by the admin before the add-drop run.|
|Allocation/Algorithm |HBS_DRAFT | This table contains the entries about draft algorithm runs.|
|Allocation/Algorithm | COURSE_ALLOCATION | This table contains the master entry about every algorithm run.|
|Allocation/Algorithm | COURSE_ALLOCATION_STUDENT | This table contains the initial position of every student during the algorithm run. This position is used to determine when a students requests get picked up during the run.|
|Allocation/Algorithm | COURSE_REQUEST | This table contains details about the student requests for each algorithm run that was run against the request by an allocation run.|
|Allocation/Algorithm | ALLOCATION_PERIOD_STATE | This table contains aggregated data about an allocation period stored as JSON. It stores details to display on the admin dash board based various allocation periods. The data is indexed using elective period id |
|Allocation/Algorithm | ALLOCATION_STATISTIC | This table contains aggregated data about an allocation run per course section. It stores information like how many enrollments where done in a course section,  the round at which the course got filled, requests in wait pool etc. This is used for reports.|
|Allocation/Algorithm | ROUND_STATISTIC | This table stores statistics with respect to an allocation run for every course section by every turn/round.|
|Enrollment | COURSE_ENROLLMENT | This table represents the students' enrollments into courses. Every enrollment is related to the elective period.|
|Enrollment | SIS_ENROLLMENT_STATUS | This table is populated by the job that exports students enrollments into SIS.|
|Settings|STUDENT_DASHBOARD | This table lets admin configure the students dashboard.|
|Settings|SETTINGS | This table lets admin configure various URLs and the synchronization mode.|
|Credits|TERM_CREDIT_LIMIT | This table contains the various credit limits configured for a term.|
|Reports|TERM_HAPPINESS_STATISTIC | <TBD>|
|Reports|REQUEST_VALIDATION_DATA | <TBD>|
|Notification|NOTIFICATION | This table stores all the notifications from the system. Data is indexed by ELECTIVE_PERIOD_ID and NOTIFICATION_TYPE. The table only stores notification code. The description of the notification is stored in resource bundles.|
|Notification|NOTIFICATION_ARGS | This table stores all the arguments that needs to be passed parse the message from the resource bundle.|
|Audit|SWITCH_USER_LOG|This table captures all the instances when an admin switches to a student login and returns back.|

##Detailed Table Structure##

###COURSE_REQUEST###
|COLUMN NAME|DATA TYPE|NULLABLE|DEFAULT DATA|COMMENTS|
|-----------|---------|--------|------------|--------|
|ID|NUMBER(19,0)|No|null|This column is a surrogate primary key for the table. It is generated using the sequence `seq_course_request_id`.|
|COURSE_ID|NUMBER(10,0)|No|null|This column denotes the course details. Foreign Keys into `COURSE.COURSE_ID`.|
|COURSE_ALLOCATION_ID|NUMBER(10,0)|No|null|This column connects the record with the parent COURSE_ALLOCATION record.|
COURSE_ENROLLMENT_ID	NUMBER(10,0)	Yes	(null)	4	(null)
COURSE_SECTION_ID	NUMBER(10,0)	No	(null)	5	(null)
DATE_CREATED	TIMESTAMP(6)	No	(null)	6	(null)
PARENT_ID	NUMBER(19,0)	Yes	(null)	7	(null)
PRIORITY	NUMBER(4,0)	No	(null)	8	(null)
PROCESSED_ROUND	NUMBER(2,0)	Yes	(null)	9	(null)
QUEUE_POSITION	NUMBER(4,0)	Yes	(null)	10	(null)
ROUND_PRIORITY	NUMBER(4,0)	Yes	(null)	11	(null)
STATUS	NUMBER(3,0)	No	(null)	12	(null)
STUDENT_ID	NUMBER(10,0)	No	(null)	13	(null)
REQUEST_TYPE	NUMBER(3,0)	No	(null)	14	(null)
SECTION_SWITCH	NUMBER(1,0)	Yes	(null)	15	(null)


