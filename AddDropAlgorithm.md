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
