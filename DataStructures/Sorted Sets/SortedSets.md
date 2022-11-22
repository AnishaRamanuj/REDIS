# SORTED SETS

- Sorted Set is an ordered collection of unique members.
- These Set members are ordered by their associated score.
- Whenever you add to a Sorted Set, you're specifying a member and a score.
- Sorted Sets keep everything sorted from the get-go.
- Sorted Sets are a good choice for priority queues, low-latency leaderboards, and secondary indexing in general.

### NOTE : Sorted sets provide the ability to perform an intersection, union and difference.(The Difference operator was added in Redis 6.2 as the ZDIFF command.)

## Why use Redis Sorted Sets?

- Responsive
- In-memory structure (that a real-time game demands.)

## To add a score member pair to a Redis Sorted Set

- use the **ZADD** command, followed by the key, the score, and the member.

``` ZADD leaders: exp 0 42 ```    ( initial score will be 0, ID of 42)

>1

## To increment a member's score by a given number
- use the **ZINCRBY** command, which takes three arguments --
the key, the increment value, and the member whose score you want to increase.

### EX. If the player with an ID of 42 defeats a monster and earns 300 experience points.

``` ZINCRBY leaders:exp 300 42 ```
>"300"

## What if we want to get a list of the top 10 players in the game?

- There are two commands that iterate over a Sorted Set in order of score and return the resulting members --

**ZRANGE and ZREVRANGE**.

- ZRANGE traverses a range of members from the lowest score to the highest score.
- ZREVRANGE does the opposite.

``` ZREVRANGE leaders:exp 0 9 WITHSCORES ```   (The 0 and 9 refer to the starting and ending indexes of our range capture.)
>"253"
>"52"
>"65"
>"85"
>"34"

## What if you wanted to display the rank of only a single member, say, on a player dashboard?

- Rank is a relative position by score of the member in the Sorted Set.
- A rank of 0 refers to the members with the lowest associated score.
- A rank of 1 represents the member with the second smallest associated score.
 
 We use the **ZRANK** command to get a member's rank from a Sorted Set.
 
 ``` ZRANK leaders: exp 42 ```
 >"11"
 - This means in a Sorted Set of length 12, the player 42 is in the highest rank, having the highest associated score.

## NOTE: This rank value isn't exactly intuitive

- so we can use the ZREVRANK command.

**ZREVRANK** gives us a ranking with a reverse sorting from highest to lowest.

``` ZREVRANK leaders:exp 42 ```
>0
(which would mean that member has the highest score.)

## ZSCORE provides the score associated with the element.

## The number of members between a range of scores is simple with ZCOUNT. 

- **ZCOUNT** will count the members between min and the max score. This is inclusive.
- Using ZCOUNT we can find the number of stations between stop number 5 and 10, that's 3 stations.


## Members can also be retrieved by score & lexicographically

- with the ZRANGEBYSCORE and the ZRANGEBYLEX commands respectively.
- We can use ZRANGEBYSCORE to find the stations between the second and the fifth stops.

## Members can be removed from sorted sets with the ZREM command.

- ZREM takes one or more elements to be removed.
- ZREM matches by the value of the element not by the score of the element.

## ZREMRANGEBYRANK removes the inclusive range of elements specified.

Example use cases for sorted sets would be a priority queue or a leaderboard.

##  Documentation for Sorted Set commands at redis.io.
 
You can find documentation [here](https://redis.io/commands/?group=sorted_set).
