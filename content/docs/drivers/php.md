+++
date = "2015-08-23T11:33:19+05:30"
draft = false
title = "PHP Driver"

+++

````
composer require bat_coder/etzelclient:dev-master

````


#### 1. publish(queuename,message,options)

This pushes a message to etzel server.The arguments required are queuename (which is the name of the queue you want to pubish to), message (which is the message you want to publish to the queue),options includes delay and expire functionality . The options argument  can be used when the message insert needs to be delayed or messaged validity needs to be expired. Options isn't an obligatory argument. The delay and expiry is taken in seconds.

Example:-
````
<?php

$etzel = new EtzelClient("ws://127.0.0.1:8080/connect");

$emails= ["abc@example.com","def@example.com","hij@example.com"];

foreach($emails as $email){
    
    $etzel->publish("group1", $email);
}
?>
````

test is the queuename,hi is the message and the delay is 0 seconds

additional options for publish:

````
    $etzel->publish('test','hi',{delay:5,expires:3600,priority:0});
````

* `delay`: The item will not be available on the queue until this many seconds have passed.
Default is 0 seconds. Maximum is 365 days(in seconds).

* `expires`: How long in seconds to keep the item on the queue before it is deleted.
Default is 0(365 days).

* `priority`: It can be either -20,0,20 (High, Medium, Low).


#### 2. subscribe(queuename,callback)

The subscribe function is fetches a message from the etzel server. The argument required are queuename which is the name of the you want to fetch the data from, callback is a custom fucntion which you have you provide. 


Example:-

````

    ec->subscribe("test",cb);

````
Here test is the queuename.
An entity fetching data from the specific queue is called a worker. You can multiple workers working on the same queue. The server facilitates load balancing amongst the workers. Fetching a message will delete the message from the queue **temporarily**(re-queued after 60 seconds). 

acknowledge(queuename,uid)

To delete it permanently , we use the acknowledge function which deletes/acknowledges a specific message from the queue. The arguments required are queuename and the id of the message you want to acknowledge.


