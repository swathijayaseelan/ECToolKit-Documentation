# ECTK Synchronization #

## Overview ##

ECTK uses/stores its data locally in a format that is optimized for the applications's use. Synchronization is the process through which ECTK gets data from Enterprise SIS DB.

The data travels through the following layers in the synchronization process before it reaches the ECTK tables.

**Data Virtualization Layer (DVL):** The data from the Enterprise SIS DB is exposed to other schema's by a set of views. These collection of read-only views is called the Data Virtualization Layer, DVL in short. 

**ECTK's Stage Views:** ECTK adds a layer of abstraction through it's own views on top of the DVL, to hide the intricate details of the DVL. This is called the *Stage Views*. These are *views of views*. 

**Synchronization Jobs:** The synchronization jobs convert the data from the stage views into the required format and dump the data into the ECTK tables. 

The below picture summarizes the transformation. 
![ECTK-SYNC](https://github.com/jganesan1/ECToolKit-Documentation/blob/master/ECTK-Sync.png)

## Synchronization ##

The synchronization happens based on the last modified date of an entity record. The last modified date is known as ***Refresh Date*** in ECTK synchronization parlance. Every stage view has refresh date. 

For synchronization, we pick only those records from the stage view, whose refresh date is greater the max refresh date of the all the existing entities. 

**Types of Synchronization:** There are two types of synchronization - *Full* and *New and Updated*. As the name suggests, the New and Updated and updates the new and updated records only. A Full synchronization not only copies and updates the new and updated records, but also deletes the deleted records. 


## Entities/Tables Involved in Synchronization ##

|S.No|Table Name| Stage View Name|Synchronization Class|
|----|----------|----------------|---------------------|
|1|ALLOCATION_PERIOD|STAGE_ACTIVITY_TASK_CONFIG|AllocationPeriodSyncService|
|2|COURSE_ENROLLMENT|STAGE_STUDENT_ENROLLMENT|CourseEnrollmentSyncService|
|3|COURSE_PREREQUSITE|stage_course_prerequisite|CoursePrerequisiteSyncService|
|4|COURSE_SECTION_FACULTY|stage_course_section_faculty|CourseSectionFacultySyncService|
|5|COURSE_SECTION|stage_course_section_activity|CourseSectionSyncService|
|6|COURSE|stage_course_activity|CourseSyncService|
|7|COURSE_UNIT|stage_course_unit|CourseUnitSyncService|
|8|ELECTIVE_PERIOD_STUDENT|stage_academic_phase_enroll|ElectivePeriodSyncService|
|9|LESSON_EVENT|stage_course_section_meeting|LessonEventSyncService|
|10|MUTUALLY_EXCLUSIVE_COURSE|stage_mutually_exclusive|MutuallyExclusiveSyncService|
|11|PERSON|stage_person|PersonSyncService|
|12|PROGRAM_SESSION|stage_program_session_activity|ProgramSessionSyncService|
|13|TERM_CREDIT_LIMIT|stage_credit_limit|TermCreditLimitSyncService|
|14|TERM|stage_term_activity|TermSyncService|
|15|UNIT|stage_unit|UnitSyncService|

## Single Synchronization Flow ##

Let us review the synchronization flow by taking the example of ```Person``` table. The next section summarizes the other sync processes.

* The PersonSyncService gets the max refresh date in the table by using the below GORM (HQL) query.
```sql
SELECT MAX(refreshDate) FROM Person
```
* Then we use another query to find out the records that have been modified after this date from ```stage_person``` view
```sql
			SELECT
				person_id AS id,
				first_name AS firstName,
				middle_name AS middleName,
				last_name AS lastName,
				email_address AS email,
				joint_degree_program_type_code AS programType,
				entry_term_acty_id AS entryTermId,
				estimated_graduation_date AS estimatedGraduationDate,
				refresh_date AS refreshDate
			FROM stage_person
			WHERE refresh_date > ?
```
* For all the records that is found from the query, it picks the corresponding ```Person``` object. 
* If the ```Person``` object is found then, the record is updated, else a new ```Person``` object is created and persisted to the ```Person``` table.
* This sync does not differentiate between the two types of the behavior. A person record is never deleted.

