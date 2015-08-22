+++
date = "2015-08-22T22:10:32+05:30"
draft = true
title = "Worker algorithm"
+++


#### AWAKE_MODE:

````

    1. Req for job
    2. if no job go to SLEEP_MODE
    3. Process the Job.
    4. Go to Step 1.
    
````
#### SLEEP MODE:

````
    1. Listen to Socket
        - If job==AVBL go to AWAKE_MODE
```` 

