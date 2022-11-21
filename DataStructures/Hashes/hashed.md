# Hashes

- Hashes are collections of field-value pairs
- look a lot like a JSON Object, a Java HashMap, or a Python Dictionary.
- Redis Hashes are also mutable.We can add, change, increment, and remove field-value pairs at any time, not just at the initial declaration.
- Hashes store field values as Strings, which means that they are flat.
- There are no nested Arrays or Objects.
- Also, we do not need to predefine field names of Redis Hashes.


### While Redis Hashes are schemaless, you can still think of them as lightweight objects or as rows in a relational database table.

- we'll use the HSET command to add a new field-value pair.

``` HSET player:42 status dazed ```
>1

## To delete a field-value pair from a Redis Hash, we use the command HDEL.

``` HDEL player:42 status  ```
>1

## To get all the fields and values from a Redis Hash, use the HGETALL command

``` HGETALL player:42 ```
>"gold"
>"hp"
>"Anisha"
>"140"

## HINCRBY,increments the value of a particular Hash field.
``` HINCRBY player:42 gold 120  ```
> 140

#### NOTE:  Most Hash commands are O(1) , which means they will always perform a task in a constant amount of time, regardless of the size of the Hash.

#### The HGETALL command is O(n) , with n being the number of fields within a Hash.

##  Documentation for Hash commands at redis.io [here](https://redis.io/commands/?group=hash).
