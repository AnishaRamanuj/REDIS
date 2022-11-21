# LISTS

- List as an ordered sequence of strings comparable to a Java ArrayList, a JavaScript array, or a Python list.
- Lists are great for storing strings, but you can also use them to implement stacks and queues.

## We push elements onto the right-hand side of the List using the RPUSH command.

``` RPUSH playlist 25 ```
>1

## remove, or pop, the songs from the left-hand side. The command to remove an element from our queue is LPOP.

``` LPOP playlist  ```
>25

## The LRANGE command returns elements within a List between a given start and end index offset.

- our starting index is 0, and our ending index is 4

```  LRANGE playlist 0 4. ```
>1)"71"

>2)"2"

>3)"53"

>4)"12"

>5)"4"

## To check the length of a Redis List, use the LLEN command.

```LLEN playlist ```
>7

- LPOP, RPUSH, and LLEN are all O(1) constant time complexity operations.
- LRANGE is O(s+n), where s is the distance of the start offset from the head, and n is the number of elements in the specified range.

## NOTE: A single List can hold over 4 billion entries.

### Need a queue?

Just use RPUSH and LPOP.

### Need a stack?
Use RPUSH and RPOP.

### Traverse a List?
Remember, LRANGE.
