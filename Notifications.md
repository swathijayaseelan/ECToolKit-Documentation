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

