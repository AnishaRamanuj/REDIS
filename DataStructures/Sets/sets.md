# SETS

- A set is an unordered collection of strings that contains **no duplicates**.
- Another important set property? **Efficient membership checks**.
- Redis sets support standard mathematical set operations, like intersection, difference, and union.

## How to add a player's ID to the players:online set.

We call the command **SADD** followed by the set name.

``` SADD players: online 42  ```
>1

## How do we go about showing how many players are online?

For that, we can use **SCARD** to get the cardinality or number of members in the set.

``` SCARD players: online   ```

>1000000000

( we have a billion players online.)

## SISMEMBER to determine whether to light up the "I'm online" button.

``` SISMEMBER player: online 42   ```

>1  

(player is online)

``` SISMEMBER player: online 32   ```

>0

(player is offline)

## Intersection of two sets is the subset of members in both sets.

 command for this is **SINTER**.
 
 ``` SINTER player: 31: friends players online   ```

>"42"

>"30"

>"52"


## REVIEW

- Sets are unordered collection of strings thst contain no duplicates
- SADD- add numbers to a set
- SCARD- tells how many members are in a set
- SISMEMBER- checks if a member is in a set
- SINTER- gives the intersection of two or more sets
- SSCAN- to get the current elements of the set.

## Documentation for Set commands at redis.io
You can check documentato [here](https://redis.io/commands/?group=set).

## NOTE: Sets are unordered, therefore we can not retrieve a value in a Set by position.  
