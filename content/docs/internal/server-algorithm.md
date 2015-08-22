+++
date = "2015-08-22T22:49:39+05:30"
draft = true
title = "Server algorithm"
+++

###### ON_SUBSCRIBE:
 
```` 
   - Spawn a process for client & attach its PID to the group.
   - Example: join_group(Qname,PID) 
````    
    
###### ON_PUBLISH:
  
````
   - IF NO DELAY -> CALL PUBLISH();
   - Else: 
     - CALL PUBLISH(); with delay
     - write this info(key:value) to disk
````

````
PUBLISH()
   - Broadcast Awake Signal to all processes in the sleep list.
   - & Remove those processes from the sleep list.
   - Spawn a process for the Queue-X if it does not exist
   - & send the Element to this process.
   - Now this Queue-X Process will accept the element
   - & also write(async) the data to disk by generating required key:value  
````
###### ON_FET_REQUEST:

````
   1. Pop the top of the Queue 
   2. if the element has expired 
        2.1 Delete element from disk
        2.2 go to step 1
   3. if the element matches with any element in the delete list: 
      3.1. remove the element from the delete list.
      3.2. Go to Step 1
   3. else Send it to the requested Client 
   4. increment the 'error_count' of the Element on Disk
   5. CALL PUBLISH(element); WITH DELAY:60
````

###### ON_ACK/DEL_REQUEST:

````
  - Delete the element from disk
  - PUSH the element to the delete list
````