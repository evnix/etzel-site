+++
date = "2015-08-27T13:11:05+05:30"
draft = false
title = "C# / .NET Driver"

+++

using NuGet Console in Visual Studio 

````
PM> Install-Package EtzelClient
````

#### Publish Example

````
class Publish
   {
       static void Main(string[] args)
       {
           Etzel.EtzelClient e = null;
           try
           {
               //specify the host
               e = new Etzel.EtzelClient("ws://192.168.0.91:8080/connect");
               
               //publish a message to the queue
               e.publish("myqueue1", "mymessage");
               
           }
           catch (Exception ex)
           {
               Console.Write(ex.Message);
           }
           finally
           {
               e = null;
           }
       }
   }
````

#### Subscribe Example

````
class Subscribe
   {
       static void Main(string[] args)
       {
           Etzel.EtzelClient e = null;
           try
           {
               //specify the host
               e = new Etzel.EtzelClient("ws://192.168.0.91:8080/connect");

               //The callback that needs to be given to the subscribe function
               Etzel.EtzelClient.Tqbacks func = delegate(Etzel.Dtpl data)
               {

                   Console.WriteLine(data.msg);
               };

               //subscribes and fetches the message from the queue
               e.subscribe("myqueue1", func);

               //don't let the main program exit,
               //so that the callback is called for new messages
               while (true)
               {
                   System.Threading.Thread.Sleep(100000);
               }

           }
           catch (Exception ex)
           {
               Console.Write(ex.Message);
           }
           finally
           {
               e = null;
           }
       }
   }

````


### Functions:

#### 1. publish(queuename,message,options)

This pushes a message to etzel server.The arguments required are queuename (which is the name of the queue you want to pubish to), message (which is the message you want to publish to the queue),options includes delay and expire functionality . The options argument  can be used when the message insert needs to be delayed or messaged validity needs to be expired. Options isn't an obligatory argument. The delay and expiry is taken in seconds.

#### 2. subscribe(queuename,callback)

The subscribe function is fetches a message from the etzel server. The argument required are queueName which is the name of the Queue you want to fetch the data from, callback is a custom fucntion which you have to provide. 


Example:-


````

    ec.subscribe("test",cb);

````

Here test is the queuename.
An entity fetching data from the specific queue is called a worker. You can multiple workers working on the same queue. The server facilitates load balancing amongst the workers. Fetching a message will delete the message from the queue **temporarily**(re-queued after 60 seconds). 

````
e.acknowledge(queuename,uid)
````

To delete it permanently , we use the acknowledge function which deletes/acknowledges a specific message from the queue. The arguments required are queuename and the id of the message you want to acknowledge.

