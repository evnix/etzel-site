+++
date = "2015-08-22T22:03:05+05:30"
draft = true
title = "request response format"

+++

All messages are sent and received in JSON format.

### Subscribe to queue

```
{
    "cmd":"SUB",
    "qname": "$Q_NAME"
}
```

### Fetch a message from Queue

```
{
    "cmd":"FET",
    "qname": "$Q_NAME"
}
```

### Publish

````
{
    "cmd":"PUB",
    "qname": "$Q_NAME",
    "message": "$message",
    "delay": 0,
    "expires": 0, 
    "priority": 0

}
````
**Optional messages' parameters:**

* `delay`: The item will not be available on the queue until this many seconds have passed.
Default is 0 seconds. Maximum is 365 days(in seconds).

* `expires`: How long in seconds to keep the item on the queue before it is deleted.
Default is 0(365 days).

* `priority`: It can be either -20,0,20 (High, Medium, Low).

### inform server that you are going to SLEEP

````
{
    "cmd":"ISLP",
    "qname": "$Q_NAME"
}
````

--------------------------------
## Response From server:


### No Queue Found

````
{
    "cmd":"nok",
    "err": "Q_NOT_FOUND"
}
````

### No Message Available in the requested Queue

````
{
    "cmd":"nomsg",
    "qname": "$Q_NAME"
}
````

### It is ok to go to sleep

````
{
    "cmd":"okslp",
    "qname": "$Q_NAME"
}
````

### Message Available in the requested Queue

````
{
    "cmd": "msg",
    "qname": "$Q_NAME",
    "uid": "$uid",
    "error_count": "$count",
    "msg": "$message"
}
````

### Wake up the client for a particular Queue

````
{
    "cmd":"awk",
    "qname": "$Q_NAME"
}
````
