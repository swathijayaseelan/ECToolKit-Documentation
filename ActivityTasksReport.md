#### Activity Task Report:  
    This Report have details about Activity Tasks, Allocation Periods and Admin Actions.
#### Queries involved:
##### Activity tasks: To display the details under Activity Tasks below query is executed.
    
      STAGE_ACTIVITY_TASK_CONFIG:
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
      
  #### Allocation Periods: To display the details under Allocation Periods below query is executed.
  
    ALLOCATION_PERIOD:
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
      
  ##### Admin Actions:To display the details under Admin Actions below query is executed. Only Notifications of Type Action(3) will be displayed.
  
      NOTIFICATIONS:
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
     
