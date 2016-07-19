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

