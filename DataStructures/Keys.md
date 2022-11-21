## KEYS

Keys are the primary way to access data values
within Redis.

Key names are unique by definition.
Key names are binary safe in Redis.

This means any binary sequence can
be used as a key, anything from a simple string like Foo,
numbers like 42, or 3.1415, or a binary value.

They can be up to 512 megabytes in size,
and that may be increased in future versions of Redis.
However, super long keys are generally not recommended.

Within a logical database, a single flat key space exists.
This means all the key names occupy the same space.
There is no automatic separation of key names
into named groups such as buckets or collections.

A logical database is identified by a zero-based index.
The default is database 0.
Within a logical database, the key names
are unique as mentioned.

But the same key name can appear in multiple logical databases,
so logical databases do provide separation of key names.

Logical databases also have a number of restrictions.
Notably, Redis cluster only supports database 0.

* the first two Redis commands. 
1. SET Key Value [Ex Seconds]
[PX miliseconds][NX][XX]
-NX is for non existence of key and XX is for existence of key
Set provides a way to store a value for a given key name.

2. GET Key
GET returns the value at the given key name.

* Redis replies with an OK response.

* CLI marks the response as string using
the double quotes convention.
-------------------------------------------------

There are two commands for getting
a list of existing key names in your Redis database.
1. The first is called KEYS.
2. The second is called SCAN.

Before moving on, it's important to understand the differences
between these commands.
----------------------------------
The KEYS command always blocks entries iterated over all keys.

NOTE-- If your database contains millions of keys,then running this command may blockthe database for a long time.
Therefore, it's never a good idea
to run the KEYS command in production.

-KEYS command can be useful for local debugging.
----------------------------
SCAN slot [MATCH pattern][COUNT count]
* The SCAN command also blocks, but it only iterates over a handful of keys at the time.
    * Iterates using a cursor
    * Returns 0 or more keys per call
    * return a slot refrence
-------------------------------------------------
## EX. Suppose we want to find all customer keys whose IDs begin with a 1.
> keys customer : 1*

----To execute SCAN, we start by giving a slot value of zero.
>SCAN 0 MATCH customer : 1*

* there will be a new slot ID to plug into the next call.
* It may take many calls, but ultimately we get the same results we got when running the KEYS command.
>SCAN 1436 MATCH customer : 1*

--SCAN will return a cursor value of 0 when it has no more keys to iterate over.

---------------------------------------------
## To remove the Key and memory associated with it.
>DEL key[key...]
-The DEL command will remove the key and the memory associated with the key.

>UNLINK key[key...]
With UNLINK, the key is unlinked--
hence the name of the command and will no longer exist.
so the UNLINK is a non-blocking command.

----------------------------------------
If you want to set the value if the key already exists.
>EXISTS key[key...]
-EXISTS will return 1 if the key exists and 0 if it does not, As you can see here.

---------------------------------
EX. Check the available tickets, the women's 100-meter final event.(In this case, 1,000 tickets are available.)
> set inventory : 100-meters-womens-final 1000 NX
OK

--Next, we try to set the value to sold out, again, with the NX parameter.
> set inventory : 100-meters-womens-final "Sold out" NX
(nil)

--Finally, we set the value to 0, this time, with the XX parameter, indicating that the key must exist before we apply the value.
>set inventory : 100-meters-womens-final 0 XX
OK

--Using GET, we can see the value is now 0.
> get inventory : 100-meters-womens-final 
"0"

# TTL(time to live) 

* Expiration times can be set in milliseconds, seconds or a UNIX timestamp.
-The TTL can be set when the key is first created or can be set afterwards.
--If want to specify time in seconds , use- EX
                             miliseconds, use- PX

--- A number of commands help manage the TTL of keys.
* Set 
	--EXPIRE key seconds
	--EXPIREAT key timestamp
	--PEXPIRE key miliseconds (If the key already exists or you want to change the expiration you do this with the PEXPIRE)
	--PEXPIREAT key miliseconds-timestamp

--- TTL for a key can be inspected using the TTL in seconds or PTTL for milliseconds. 
* Examine
	--TTL key
	--PTTL key 

---  Finally a TTL can be removed with the PERSIST command.
* Remove
	--PERSIST key( Using the PERSIST command we can then remove the TTL on the key to ensure the key is retained)

# TO BE RECAP

REDIS key Names
1. Unique key 
2. Binary Strings
3. Flat namespace
4. can be upto 512 megabytes
5. presence/absence can be used to determine if a set occurs
-automatic expiration of keys through a TTL.
