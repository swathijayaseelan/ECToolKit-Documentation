#### Add Drop Algorithm
##### Types of Add Drop Request:
- Add
- Drop
- Add with Alternatives.

Class Involved:
- AddDropContextProcess.java - Contains the core logic of the Algorithm.

Below is the process involved when Add Drop Algorithm is run by Admin.

#### Step 1: 
-     Drops are processed. Below flowchart describes the only the Drop process.

![Alt text](https://raw.githubusercontent.com/swathijayaseelan/ECToolKit-Documentation/47efcd2fbd063f7f53fa8d9731bdc3f0dc421f02/ProcessDropFlow.jpg "Process Drops FlowChart")      

#### Step 2: 
- Add course requests of the students to new request pool or temporary subset of existing prioritization queue, request queue or request pool depending on value of addToTemporarySubset flag. 
- When adding to new request pool check for the presence of student in existing prioritization queue, request queue or request pool and if found student won't be added to new request pool.

![Alt text](https://raw.githubusercontent.com/swathijayaseelan/ECToolKit-Documentation/afc7845395f7170b9aff6e0a1e1269a902037406/AddRequestPoolDiagram.jpeg "Add Request Pool FlowChart")  

#### Step 3: 
- Get the Round Number.

#### Step 4:
- Maximum number of iteration in Add Drop is 3. 
- So iterate the students for 3 iterations.

![Alt text](https://raw.githubusercontent.com/swathijayaseelan/ECToolKit-Documentation/78bd2ba276208be562022d52dc80aec402961ce4/AddDropDiagram.jpeg "AddDropProcessing FlowChart")  

#### Request Status:

|Status|Corresponding value|
|--------------------- |---------|
|UNPROCESSED         | 0    
|ASSIGNED            | 1 
|ADDED               | 2  
|DROPPED             | 3
|OTHER OPTION ADDED  | 4    
|WAIT POOL           |100
|TIME CONFLICT       |101
|COURSE CANCELLED    |200
|COURSE SECTION CANCELLED |201
|DUPLICATE    |202
|REQUEST LIMIT EXCEEDED |203
|NOT ENROLLED |204
|ALREADY ENROLLED |205
|ALREADY ENROLLED IN SECTION OF SAME COURSE |206
|INVAID |207
|N/A |208
|CREDIT LIMIT EXCEEDED |209
|XY CREDIT LIMIT EXCEEDED | 210
|PREREQUISITE MISSING  |211
|BLOCKED BY MUTUALLY EXCLUSIVE COURSE |212
|BLOCKED BY YOUR EXCLUSION SET | 213
|DEPENDANT COURSE ENROLLED |214
|APPLICATION ONLY COURSE |215
|PROCESSING ENROLLEMENT |216
|STUDENT WITHDRAWN |217

	
