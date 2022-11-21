# Strings


Redis strings are binary safe sequences of bytes.
- It can have Integers, binary values, comma-separated values, serialized JSON.
- And since they're binary safe, you can even store larger objects, such as images, videos, documents and sound.

The most common use is for caching: API responses, session storage, HTML pages.
Redis strings are also great for implementing counters, as there is built in support for incrementing and decrementing integer and floating point values.

### To create a string in Redis, you'll use the *SET* command.

*``` SET <KEY> <VALUE>  ```*

- For example, let's create a time zone entry
for a user of an application that we're building.

*``` SET use user:101:time-zone UTC-8 ```*                       (I'll use user:101:time-zone as the key and UTC 8 as the value.)
>OK 

### To retrieve a Redis string, you use the *GET* command,
 
 *``` GET use user:101:time-zone UTC-8 ```*
>OK 

### *TTL* returns the number of seconds remaining before the key expires.

### With the *INCR* and *INCRBY* commands, you can increment a key's value by one or by a specified number.

NOTE - If a data structure doesn't exist, then it will be created the moment you write to it.


 ## Documentation for Strings commands
 
 see documentation [here](https://redis.io/commands/?group=string).
 
 ##  TYPE command
 
 - IT returns the data type of the structure stored at the key.
 see documentation [here](https://redis.io/commands/type).
 
 ##  OBJECT command
 
 - We can also check the encoding of the value with the OBJECT command.
 see documentation [here](https://redis.io/commands/object).
 
 # REDIS STRINGS

- store plain old strings, numerical values, serialized JSON, and anything that can be represented in binary
- commonly used for caching when combine with EXPIRE
- Store and manipulate numerical values   
- Encoding verified before command execution
 
