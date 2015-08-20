+++
date = "2015-08-18T10:35:58+05:30"
draft = true
title = "Etzel Server"

+++

A Fast & Reliable open source Job delegation & queueing server. 


![Etzel Server](/images/etzel.png)

Etzel is built for Robust messaging between applications. It has built-in support for load-balancing and fault tolerance. 

### Example:

Let us define some workload i.e. to send emails using PHP(client)


````javascript
<?php

$etzel = new EtzelClient("ws://127.0.0.1:8080/connect");

$emails= ["abc@example.com","def@example.com","hij@example.com"];

foreach($emails as $email){
	
	$etzel->publish("group1", $email);
}

````
<!-- ?> -->
Now, Let us process those emails using nodejs(worker)

````javascript
ec=new EtzelClient("ws://localhost:8080/connect");

ec.onopen=function(){
	
	ec.subscribe("group1",sendMail);
}

function sendMail(data){

		sendmessage(data.msg,"Subject","Message");
		ec.acknowledge(data.uid); //delete it

}

````

**Did you know?** 
you could have hundreds of workers connected to Etzel to do the processing and Etzel will automatically balance the load between them. 

Etzel Instances are light weight, Hence you can have multiple Etzel instances running in parallel in the same or different server.

**What if a worker dies?**

Etzel will route the messages to the workers that are alive and re-send incomplete tasks to other workers.

**What if all the workers die?**

Etzel will keep the messages until a worker is available.

