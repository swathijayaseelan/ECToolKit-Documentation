# ECTK Synchronization #

## Overview ##

ECTK uses/stores its data locally in a format that is optimized for the applications's use. Synchronization is the process through which ECTK gets data from Enterprise SIS DB.

The data travels through the following layers in the synchronization process before it reaches the ECTK tables.

**Data Virtualization Layer (DVL):** The data from the Enterprise SIS DB is exposed to other schema's by a set of views. These collection of read-only views is called the Data Virtualization Layer, DVL in short. 

**ECTK's Stage Views:** ECTK adds a layer of abstraction through it's own views on top of the DVL, to hide the intricate details of the DVL. This is called the *Stage Views*. These are *views of views*. 

**Synchronization Jobs:** The synchronization jobs convert the data from the stage views into the required format and dump the data into the ECTK tables. 

The below picture summarizes the transformation. 
![ECTK-SYNC](https://github.com/jganesan1/ECToolKit-Documentation/blob/master/ECTK-Sync.png)