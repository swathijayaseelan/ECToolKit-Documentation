#### Errors Report:
-	Report holds two different kinds of Errors. Credit Errors & Course Errors.

#### Credit Error Details: 
- Below are the type of checks made in the student schedule and errors are captured.

|Type of Error|Messages|Comments|
|--------------------- |--------------------- |-----------------|
|Credit Errors         | check for excess     | For ProgramType MBA. When TermCredits >=Min termCredits of the schedule and TermCredits < Max of termCredits
|Credit Errors         |not enough class credits|If currentPeriod is 'ADD_DROP' and ClassCredits >= Class Credits of the Student Schedule.   
|Credit Errors         |excessive term credits|When the student schedule have more than the term credits.
|Credit Errors         |not enough term credits|When the student schedule have less than the term credits.
|Credit Errors         |excessive X credits|When the student schedule have more than the X credits.
|Credit Errors         |excessive Y credits|When the student schedule have more than the Y credits.
                                               
#### Course Error Details: 
- Below are the type of checks made in the student schedule and errors are captured.

|Type of Error|Messages|Comments|
|--------------------- |--------------------- |-----------------|
|Course Errors         | has duplicate course<<courseNumbers>> and <<sections>| Applicable only to ClassRoom courses. If the courseNumber already exists in the enrolled Courses.And it checks for the CourseSections, if already exists in the enrolled Course Section.
|Course Errors           |has mutually exclusive courses<<CourseNumber>> and <<sections>>|If the course which is enrolled exists in Mutually exclusive set.And it checks for the CourseSections, if already exists in the enrolled Course Section.
|Course Errors           |missing prerequisite for course <<Course Numbers>>|When the student schedule have the prerequisite courses missing.
|Course Errors           |has timing conflict for courses <<Course Numbers>> and <<sections>>|If the course which is enrolled conflicts with any other courses.And it checks for the CourseSections, if there is any time conflicts with any other course sections.

Json columns requires special handling and the Total Request, fall, January & spring are calculated against the Students based on the foreign key ID.
### Tables Involved:
•	EC_PHASE
•	PERSON
•	STUDENT_REQUESTS
## Classes Involved:
### JS/HTML Files:
•	admin.js
•	BasicReportCtrl.js
•	ReportService.js
•	lowActivity.html

### Controller: (Rest Controllers)
•	PeriodReportingController.groovy:
      Based on the request Mapping corresponding PeriodReportingService is involved.
•	PeriodExportingController.groovy:
      Based on the request Mapping corresponding PeriodExportingService is involved. This controller is invoked while the user tries to download the data via ‘EXPORT’ button.

### Service:
•	PeriodReportingService.groovy
This service communicates with the database and constructs the data which are needed to be displayed in the Report

### Basic Report Flow:

![Alt text](https://raw.githubusercontent.com/swathijayaseelan/ECToolKit-Documentation/master/BasicReportFloe.png?_sm_au_=i4sfNDn0HvvfvS2k "Basic Report Flow")

Queries involved:
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
PERSON: Only Active Students are retrieved which includes Test Students as well.(withdrawn is null)
select
        this_.elective_period_id as elective_period_id1_15_1_,
        this_.student_id as student_id2_15_1_,
        this_.refresh_date as refresh_date3_15_1_,
        this_.withdrawn as withdrawn4_15_1_,
        person2_.id as id1_23_0_,
        person2_.biography as biography2_23_0_,
        person2_.date_created as date_created3_23_0_,
        person2_.email as email4_23_0_,
        person2_.entry_term_id as entry_term_id5_23_0_,
        person2_.estimated_graduation_date as estimated_graduati6_23_0_,
        person2_.first_name as first_name7_23_0_,
        person2_.first_time_tour as first_time_tour8_23_0_,
        person2_.interests as interests9_23_0_,
        person2_.invalid as invalid10_23_0_,
        person2_.last_name as last_name11_23_0_,
        person2_.last_updated as last_updated12_23_0_,
        person2_.middle_name as middle_name13_23_0_,
        person2_.phase_involved as phase_involved14_23_0_,
        person2_.program_type as program_type15_23_0_,
        person2_.refresh_date as refresh_date16_23_0_,
        person2_.sync_error_message as sync_error_messag17_23_0_,
        person2_.title as title18_23_0_,
        person2_.units as units19_23_0_
    from
        elective_period_student this_
    inner join
        person person2_
            on this_.student_id=person2_.id
    where
        this_.elective_period_id=?
        and this_.withdrawn is null
```
```
STUDENT_REQUESTS:
select
        this_.student as student1_30_0_,
        this_.elective_period as elective_period2_30_0_,
        this_.requests_json as requests_json3_30_0_
    from
        student_requests this_
    where
        this_.elective_period=?
```

