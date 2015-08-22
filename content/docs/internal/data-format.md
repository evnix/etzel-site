+++
date = "2015-08-22T23:02:31+05:30"
draft = true
title = "Data format"

+++

### Queue Element format in Memory

````
error_count|expires|UidSize|uid|Item

Size of each block in bits:
<<error_count:8>>,<<Expires:64>>,<<Uid_size:16>>,Uid,Msg
````

### Queue element format on disk
The queue elements are stored in a key value store in the following format.
````
1. DATA

let us divide DATA which is made up of a key and value.

2. Key: Value

divide them further

3. Qname-uid:  error_count|Delay|expires|Item

Qname: Variable length text
Uid: 14-18 bytes
error_count: 8 bits 
delay: 64 bits
expires: 64 bits
Item: Variable lenght text

````