### Errors Report:
-	Report holds two different kinds of Errors. Credit Errors & Course Errors.

##### Credit Error Details: 
- Below are the type of checks made in the student schedule and errors are captured.

|Type of Error|Messages|Comments|
|--------------------- |--------------------- |-----------------|
|Credit Errors         | check for excess     | For ProgramType MBA. When TermCredits >=Min termCredits of the schedule and TermCredits < Max of termCredits
|Credit Errors         |not enough class credits|If currentPeriod is 'ADD_DROP' and ClassCredits >= Class Credits of the Student Schedule.   
|Credit Errors         |excessive term credits|When the student schedule have more than the term credits.
|Credit Errors         |not enough term credits|When the student schedule have less than the term credits.
|Credit Errors         |excessive X credits|When the student schedule have more than the X credits.
|Credit Errors         |excessive Y credits|When the student schedule have more than the Y credits.
                                               
##### Course Error Details: 
- Below are the type of checks made in the student schedule and errors are captured.

|Type of Error|Messages|Comments|
|--------------------- |--------------------- |-----------------|
|Course Errors         | has duplicate course and sections| Applicable only to ClassRoom courses. If the courseNumber already exists in the enrolled Courses.And it checks for the CourseSections, if already exists in the enrolled Course Section.
|Course Errors           |has mutually exclusive courses and sections |If the course which is enrolled exists in Mutually exclusive set.And it checks for the CourseSections, if already exists in the enrolled Course Section.
|Course Errors           |missing prerequisite for courses|When the student schedule have the prerequisite courses missing.
|Course Errors           |has timing conflict for courses and sections|If the course which is enrolled conflicts with any other courses.And it checks for the CourseSections, if there is any time conflicts with any other course sections.

Json columns requires special handling and the Total Request, fall, January & spring are calculated against the Students based on the foreign key ID.
##### Tables Involved:
-	EC_PHASE
-	COURSE_ENROLLMENT
-	ALLOCATION_PERIOD

##### Classes Involved:
###### JS/HTML Files:
- admin.js
- ErrorsCtrl.js
- ReportService.js
- errors.html

##### Controller: (Rest Controllers)
- PeriodReportingController.groovy:
      Based on the request Mapping(@RequestMapping(value='/errors', method=GET))corresponding PeriodReportingService is involved.
- PeriodExportingController.groovy:
      Based on the request Mapping corresponding PeriodExportingService is involved. 
      This controller is invoked while the user tries to download the data via ‘EXPORT’ button.

##### Service:
-	PeriodReportingService.groovy:
      This service communicates with the database and constructs the data which are needed to be displayed in the Report

##### Data Layer:
- Schedule.groovy:
      Data(Report Details) is constructed in Schedule.groovy. Details are segregated into credit/course errors. Above checks are made and details are collected into the List to be displayed and to export.

##### Basic Report Flow:

![Alt text](https://raw.githubusercontent.com/swathijayaseelan/ECToolKit-Documentation/master/BasicReportFloe.png?_sm_au_=i4sfNDn0HvvfvS2k "Basic Report Flow")

##### Queries involved:
```
EC_PHASE:
select
        ecphase0_.id as id1_12_0_,
        ecphase0_.active as active2_12_0_,
        ecphase0_.allocation_period_chart_json as allocation_period_3_12_0_,
        ecphase0_.allocation_periods_json as allocation_periods4_12_0_,
        ecphase0_.completed as completed5_12_0_,
        ecphase0_.courses_json as courses_json6_12_0_,
        ecphase0_.current_period_json as current_period_jso7_12_0_,
        ecphase0_.demand_available as demand_available8_12_0_,
        ecphase0_.elective_period_id as elective_period_id9_12_0_,
        ecphase0_.end_date as end_date10_12_0_,
        ecphase0_.event_start_times_json as event_start_times11_12_0_,
        ecphase0_.filters_json as filters_json12_12_0_,
        ecphase0_.mutually_exclusives_json as mutually_exclusiv13_12_0_,
        ecphase0_.name as name14_12_0_,
        ecphase0_.preregistration_completed as preregistration_c15_12_0_,
        ecphase0_.prerequisites_json as prerequisites_jso16_12_0_,
        ecphase0_.program_session_id as program_session_i17_12_0_,
        ecphase0_.program_session_year as program_session_y18_12_0_,
        ecphase0_.sections_json as sections_json19_12_0_,
        ecphase0_.start_date as start_date20_12_0_,
        ecphase0_.students_json as students_json21_12_0_,
        ecphase0_.term_credit_limits_json as term_credit_limit22_12_0_,
        ecphase0_.terms_json as terms_json23_12_0_,
        ecphase0_.urls_json as urls_json24_12_0_,
        ecphase0_.xreg_sections_json as xreg_sections_jso25_12_0_
    from
        ec_phase ecphase0_
    where
        ecphase0_.id=?
```
```
COURSE_ENROLLMENT:
 select
     courseenro0_.student_id as col_0_0_,
     courseenro0_.course_section_id as col_1_0_
 from
     course_enrollment courseenro0_
 where
     (
         courseenro0_.program_session_year=?
         and courseenro0_.program_id=?
         or courseenro0_.elective_period_id=?
     )
     and (
         courseenro0_.date_dropped is null
     )
```
```
ALLOCATION_PERIOD:
select
    allocation0_.id as id1_0_0_,
    allocation0_.active as active2_0_0_,
    allocation0_.allocation_date as allocation_date3_0_0_,
    allocation0_.course_allocation_id as course_allocation_4_0_0_,
    allocation0_.date_created as date_created5_0_0_,
    allocation0_.elective_period_id as elective_period_id6_0_0_,
    allocation0_.end_date as end_date7_0_0_,
    allocation0_.last_updated as last_updated8_0_0_,
    allocation0_.name as name9_0_0_,
    allocation0_.refresh_date as refresh_date10_0_0_,
    allocation0_.sequence_name as sequence_name11_0_0_,
    allocation0_.start_date as start_date12_0_0_,
    allocation0_.allocation_period_type as allocation_period13_0_0_
from
    allocation_period allocation0_
where
    allocation0_.id=?
```

