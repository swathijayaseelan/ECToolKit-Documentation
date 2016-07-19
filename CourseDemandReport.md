#### Course Demand Report:
-	To get the demand of the course/course section. This report is executed by Admin. The report gets the data after the Preregistration entry period.
-	Before the completion of Pre-Registration period this data would not give up any results.

#### Report Details

|Report Header|Table Columns| Table |Comments|
|--------------------- |--------------------- |-----------------|-------|
|Term|sectionJSON|EC_PHASE|From sectionJSON -> term -> name
|CourseName|sectionJSON|EC_PHASE|From sectionJSON -> Course -> longName
|Course#|sectionsJSON|EC_PHASE| From SectionsJSON -> Course -> courseNumber
|Section|sectionsJSON|EC_PHASE|From SectionsJSON -> name
|Faculty|sectionsJSON|EC_PHASE|From SectionsJSON -> facultyMembers
|Credits|sectionsJSON|EC_PHASE|From SectionsJSON -> Course -> credits
|MBA Capacity|sectionJSON|EC_PHASE|From SectionsJSON -> mbaCapacity
|Total Capacity|sectionJSON|EC_PHASE|From SectionsJSON -> totalCapacity
|Meeting Time|sectionJSON|EC_PHASE|From SectionsJSON -> primaryEvent
|Other Events|sectionJSON|EC_PHASE|From SectionsJSON -> otherEvents
|Requests|requests|ALLOCATION_STATISTICS
|WaitPool|queued_requests|ALLOCATION_STATISTICS
|Enrollments|enrollments|ALLOCATION_STATISTICS
|Filled at Round|filled_at|ALLOCATION_STATISTICS

#####  Tables Involved:
-	EC_PHASE.
-	ALLOCATION_STATISTICS.
-	COURSE_ALLOCATION.

#### Classes Involved:
##### JS/HTML Files:
-	admin.js.
-	BasicReportCtrl.js.
-	ReportService.js.
-	Report.js (modifies the URL from courseDemand to CourseSectionDemand)
-	courseDemand.html

#####  Controller: (Rest Controllers)
•	PeriodReportingController.groovy:
      Based on the request Mapping(@RequestMapping(value='/courseSectionDemand', method=GET)) corresponding PeriodReportingService is involved.
•	PeriodExportingController.groovy:
      Based on the request Mapping corresponding PeriodExportingService is involved. This controller is invoked while the user tries to download the data via ‘EXPORT’ button.

#####  Service:
•	PeriodReportingService.groovy
This service communicates with the database and constructs the data which are needed to be displayed in the Report

#### Queries involved:
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
COURSE_ALLOCATION:
select
     *
 from
     ( select
         this_.id as id1_4_1_,
         this_.active_student_count as active_student_cou2_4_1_,
         this_.allocation_period_type as allocation_period_3_4_1_,
         this_.credit_happiness as credit_happiness4_4_1_,
         this_.date_created as date_created5_4_1_,
         this_.deleted as deleted6_4_1_,
         this_.demand as demand7_4_1_,
         this_.elective_period_id as elective_period_id8_4_1_,
         this_.enrollment_version as enrollment_version9_4_1_,
         this_.inactive_student_count as inactive_student_10_4_1_,
         this_.last_updated as last_updated11_4_1_,
         this_.name as name12_4_1_,
         this_.request_happiness as request_happiness13_4_1_,
         this_.total_rounds as total_rounds14_4_1_,
         this_.translation_status as translation_statu15_4_1_,
         this_.allocation_type as allocation_type16_4_1_,
         this_1_.processed_at as processed_at2_18_1_,
         case
             when this_1_.id is not null then 1
             when this_.id is not null then 0
         end as clazz_1_,
         electivepe2_.id as id1_14_0_,
         electivepe2_.active as active2_14_0_,
         electivepe2_.clone as clone3_14_0_,
         electivepe2_.completed as completed4_14_0_,
         electivepe2_.current_period_id as current_period_id5_14_0_,
         electivepe2_.date_created as date_created6_14_0_,
         electivepe2_.demand_available as demand_available7_14_0_,
         electivepe2_.end_date as end_date8_14_0_,
         electivepe2_.last_updated as last_updated9_14_0_,
         electivepe2_.name as name10_14_0_,
         electivepe2_.phase_id as phase_id11_14_0_,
         electivepe2_.preregistration_completed as preregistration_c12_14_0_,
         electivepe2_.program_session_id as program_session_i13_14_0_,

         electivepe2_.start_date as start_date15_14_0_
     from
         course_allocation this_
     left outer join
         hbs_draft this_1_
             on this_.id=this_1_.id
     inner join
         elective_period electivepe2_
             on this_.elective_period_id=electivepe2_.id
     where
         this_.elective_period_id=?
         and this_.demand=? )
 where
     rownum <= ?
```
```
ALLOCATION_STATISTCS:
select
     this_.id as id1_2_0_,
     this_.allocation_period_id as allocation_period_2_2_0_,
     this_.alternative_requests as alternative_reques3_2_0_,
     this_.course_allocation_id as course_allocation_4_2_0_,
     this_.course_section_id as course_section_id5_2_0_,
     this_.drop_requests as drop_requests6_2_0_,
     this_.drops as drops7_2_0_,
     this_.enrollments as enrollments8_2_0_,
     this_.filled_at as filled_at9_2_0_,
     this_.initial_enrollments as initial_enrollmen10_2_0_,
     this_.queued_requests as queued_requests11_2_0_,
     this_.requests as requests12_2_0_
 from
     allocation_statistic this_
 where
     this_.course_allocation_id=?

```
