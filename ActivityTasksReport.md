#### Activity Task Report:  
    This Report have details about Activity Tasks, Allocation Periods and Admin Actions.

#### Tables and Views Involved:
 -   STAGE_ACTIVITY_TASK_COFIG.
 -   ALLOCATION_PERIOD.
 -   NOTIFICATIONS.

#### VIEWS involved:  
```
STAGE_ACTIVITY_TASK_CONFIG: Basically view gets data from SIS tables. Below are the SIS tables involved

ACTIVITY_TASK 
ACTIVITY_TASK_CONFIGURATION
ACTIVITY_TASK_REGISTRY
BT_ACTY


SELECT ATC.ACTIVITY_TASK_CONFIG_ID,
        AT.ACTIVITY_TASK_ID,
           AT.ACTIVITY_TASK_CODE,
           AT.ACTIVITY_TASK_NAME,
           ATC.ACTY_ID,
           A.ACTY_TYPE_CODE,
           ATC.START_DATE_TIME,
           ATC.END_DATE_TIME,
           CASE
              WHEN (   (AT.UPDATE_DATE >= ATC.UPDATE_DATE OR ATC.UPDATE_DATE IS NULL)
                    OR (AT.UPDATE_DATE >= A.ACTY_DATE OR A.ACTY_DATE IS NULL))
              THEN
                 AT.UPDATE_DATE
              WHEN (   (ATC.UPDATE_DATE >= AT.UPDATE_DATE OR AT.UPDATE_DATE IS NULL)
                    OR (ATC.UPDATE_DATE >= A.ACTY_DATE OR A.ACTY_DATE IS NULL))
              THEN
                 ATC.UPDATE_DATE
              WHEN (   (A.ACTY_DATE >= ATC.UPDATE_DATE OR ATC.UPDATE_DATE IS NULL)
                    OR (A.ACTY_DATE >= AT.UPDATE_DATE OR AT.UPDATE_DATE IS NULL))
              THEN
                 A.ACTY_DATE
              ELSE
                 NULL
           END
      FROM SISMGR.ACTIVITY_TASK AT,
           SISMGR.ACTIVITY_TASK_CONFIGURATION ATC,
           SISMGR.ACTIVITY_TASK_REGISTRY ATR,
           ENTMGR.BT_ACTY A
     WHERE     AT.ACTIVITY_TASK_ID = ATC.ACTIVITY_TASK_ID
           AND ATC.ACTY_ID = A.ACTY_ID
           AND ATR.ACTIVITY_TASK_ID = AT.ACTIVITY_TASK_ID
           AND ATR.APPN_PURPOSE_TYPE_CODE = 'ECTK'
```
#### Queries involved: 
#### Activity tasks: To display the details under Activity Tasks below query is executed.
```
SELECT
        activity_task_id AS id,
        activity_task_code AS code,
        activity_task_name AS name,
        start_date_time AS startDate,
        end_date_time AS endDate
    FROM
        stage_activity_task_config
    WHERE
        acty_id = ?
    ORDER BY
        start_date_time
```
#### Allocation Periods: To display the details under Allocation Periods below query is executed.
```
select
        allocation0_.elective_period_id as elective_period_id6_14_0_,
        allocation0_.id as id1_0_0_,
        allocation0_.id as id1_0_1_,
        allocation0_.active as active2_0_1_,
        allocation0_.allocation_date as allocation_date3_0_1_,
        allocation0_.course_allocation_id as course_allocation_4_0_1_,
        allocation0_.date_created as date_created5_0_1_,
        allocation0_.elective_period_id as elective_period_id6_0_1_,
        allocation0_.end_date as end_date7_0_1_,
        allocation0_.last_updated as last_updated8_0_1_,
        allocation0_.name as name9_0_1_,
        allocation0_.refresh_date as refresh_date10_0_1_,
        allocation0_.sequence_name as sequence_name11_0_1_,
        allocation0_.start_date as start_date12_0_1_,
        allocation0_.allocation_period_type as allocation_period13_0_1_
    from
        allocation_period allocation0_
    where
        allocation0_.elective_period_id=?
```
#### Admin Actions:To display the details under Admin Actions below query is executed. Only Notifications of Type Action(3) will be displayed.
```
select
        this_.id as id1_21_0_,
        this_.acknowledged as acknowledged2_21_0_,
        this_.code as code3_21_0_,
        this_.date_created as date_created4_21_0_,
        this_.default_message as default_message5_21_0_,
        this_.elective_period_id as elective_period_id6_21_0_,
        this_.last_updated as last_updated7_21_0_,
        this_.person_id as person_id8_21_0_,
        this_.notification_type as notification_type9_21_0_,
        args2_.notification_id as notification_id1_21_2_,
        args2_.arg as arg2_22_2_,
        args2_.idx as idx3_2_
    from
        notification this_
    left outer join
        notification_args args2_
            on this_.id=args2_.notification_id
    where
        (
            (
                this_.elective_period_id=?
                and this_.notification_type=?
            )
            and this_.person_id is null
        )
    order by
        this_.date_created desc

```
