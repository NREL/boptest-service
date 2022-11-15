

# Redis Caching

BOPTEST-Service currently uses Redis as a database for:
1. Storing test metadata.
2. Storing the current values of test control points. 

The purpose of this document is to define the organization of object keys used in Redis. We define the organizational structure for both storing test metadata as well as for storing the values of control points. Redis is not intrinsically hierarchical (beyond the hash key field:value pair layer), however `:` characters used in key names are conventionally treated as delimiters, and BOPTEST-Service uses this delimiter for organizational purposes.

## Test metadata:

Currently, for each test, REDIS stores the following metadata as a hash with the test-id as key and testcase name and current status as values. 
For example:

    "9028197e-1d18-4a58-a6ba-96660c50fb7a" = {status:"Running", testcaseid:"testcase_1"}

We intend to change the structure of the key to include the user-id, as seen here:

    users:john:tests:"9028197e-1d18-4a58-a6ba-96660c50fb7a" = {status:"Running", testcaseid:"testcase_1"}

 
This will help easily identify which user started each test just by the key. 

**What is the effect of key length on performance?**
For our proposed key-length, nothing significant. [We run tests](https://colab.research.google.com/drive/11puTp6noWgdqJgo51Dx42VyazmiZwgbf?usp=sharing) for the current and proposed keys for hset and hget commands. 10^9 keys are hset and hget with values that are like current BOPTEST metadata. We don't observe any significant difference in performance.  


## User specific test IDs

We also intend to make a new REDIS set which only contains the tests associated with each user. 

    users:john:tests =  
    [  
    "9028197e-1d18-4a58-a6ba-96660c50fb7a",  
    "9028197e-1d18-4a58-a6ba-96660c50fb7b",  
    ]

**Why not query from the metadata keys?** 
REDIS will allow us to query all the tests associated with the user from the keys of the metadata hash. This can be done by setting appropriate patterns and using the [KEYS](https://redis.io/commands/keys/) command. But this is an O(N) operation, where N is the number of all tests of all users. 

Creating a separate set for each user's test_id's helps us query all the test_id's with an [SMEMBERS](https://redis.io/commands/smembers/) O(N) command, where N is the number of the user's tests, which could be much faster, depending on the size of the set. 

## Test control points and associated metadata

Control points, each step of the simulation, and the metadata associated with each of the control points are communicated between the web server and the worker processes via the Redis PubSub system. 

The web server sends requests by publishing to a requests channel. The request channel is named in the format \<testid>:request. For example: `85e01d70-8755-41ab-a229-3c01f6db4ea1:request`.
The worker process listens for any request by being subscribed to this channel. 

Once the worker process has a response ready, it publishes the response to a response channel. The response channel has a name in the format \<testid>:response. For example:  `85e01d70-8755-41ab-a229-3c01f6db4ea1:response`. The web server is subscribed to this response channel and listens till it gets the correct message.
