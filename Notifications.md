Tables Involved:

•	NOTIFICAION
•	NOTIFICATION_ARGS

Javascript/html files Involved:
These files handles the display of the Notifications and the Information which is post to all the EC Students.

•	Notification.js
•	notificationService.js
•	notifications.html

Classes Involved:

•	NotificationService.groovy
•	NotificationController.groovy
•	messages_en.properties
•	NotificationType.java

NotificationController.grrovy:
This acts as a Rest Controller. Based on the request Mapping corresponding methods are invoked which in turn invokes NotificationService.groovy

NotificationService.grrovy:
This class is invoked from various other classes which are involved in Synchronization Process (Automatic / Manual).
This class contains methods which handles different Notification Types (ERROR, WARNING, INFO, EVENT, and ACTION) and finally this class inserts the Notifications into NOTIFICATION & NOTIFICATION_ARGS table.
Some of the files where notificationService is Autowired is given below

messages_en.properties:
Properties files which holds all the messages which needs to be inserted into the DEFAULT MESSAGE column of NOTIFICATION table.

NotificationType.java:
This JAVA file contains all Notification Types which are provided in the enum.

ERROR	- 1	

WARNING	- 2	

ACTION	- 3	- Displayed under Notifications.

EVENT	- 4 - None of the Notifications in the application is of Event(Notification Type).	

INFO	- 5	- Displayed under Notifications.


Below are the notifications in ECTK:

1.	notification.activate.accomplished -	INFO - On Success of the Elective Period activate during Sync Process.

2.	notification.activate.tooManyActive - ERROR -	When more than two active elective periods.(Sync Process)

3.	notification.activate.overlapping -	ERROR	- When there is overlapping in the elective periods(Inactive Periods).(Sync Process)

4.	notification.activate.notCompleted - ERROR - On failure of the Elective Period activate during Sync Process.

5.	notification.course.cancelled -	WARNING	- During the Sync Process of Course. 

6.	notification.courseSection.cancelled - WARNING -	During the Sync Process of CourseSection.

7.	notification.send.course.cancelled.failed	- ERROR	- During failure of the Notification which is supposed to be sent as the notification when any of the Course is cancelled.

8.	notification.send.courseSection.cancelled.failed	- ERROR	- During failure of the Notification which is supposed to be sent as the notification when any of the CourseSection is cancelled.

9.	notification.send.students.successful	- INFO	- When admin Posts some information to all EC Students. This notification is inserted upon successful notification to all students.

10.	notification.run.created	- INFO - On Run Creation.

11.	notification.run.finished	- INFO	- Nowhere called/invoked.

12.	notification.run.failed	- ERROR	- Nowhere called/invoked.

13.	notification.generateDemand.finished	- ACTION	- When admin clicks on ‘GENERATE DEMAND DATA’ button.

14.	notification.translate.finished	- ACTION	- On Success of Translate Process (TRANSLATE button)

15.	notification.generateDemand.failed -	ERROR -	When ‘GENERATE DEMAND DATA ‘failed.

16.	notification.generateDemand.finalize.failed -	WARNING	 - On Failure of the ‘GENERATE DEMAND Process/failure of the notification which is supposed to be send after completion of the ‘GENERATE DEMAND Process.

17.	notification.translate.failed -	ERROR -	On failure of Translate Process.( TRANSLATE button)

18.	notification.translate.finalize.failed -	WARNING -	On Failure of the Translate Process/failure of the notification which is supposed to be send after completion of the Translate Process.

19.	notification.translate.enrollments.timestamp.mismatch -	ERROR	- When the courseAllocation version is different from the version which is present in stage_course_activity and allocation is invalid.

20.	notification.translate.enrollments.sync.finished	- INFO -	On Success of Enrollments in Sync with SIS (Translate button).

21.	notification.translate.enrollments.sync.failed - ERROR -	On failure of Enrollments in SIS (Translate button).

22.	notification.translate.courseSection.capacity.overflow -	ERROR	- During Translate Process when the total is more than the capacity. Total is calculated by
e.enrolled + (e.enrollments - e.drops).
Here e is the details of the allocation.

23.	notification.translate.courseSection.capacity.underflow -	ERROR	 - During Translate Process, When no of drops is more than the enrolled.

24.	notification.enrollments.mismatch.sync.finished -	INFO - On Success of the ‘Enrollments in Sync.’

25.	notification.enrollments.mismatch.sync.failed	- ERROR -	On Failure of the ‘Enrollments in Sync’

