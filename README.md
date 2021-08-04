# Rate-limiter-using-redis

Goal:- To implement a service s.t. it act as rate limiter i.e. it allows only 10 calls per min.

We can implement rate limiter using two redis command **INCR** and **EXPIRE**.
We will create a redis key every minimute per API. Also, we are going to expire these keys after a minute.

We can store the details for each API using a {key, value} pair, where key = "[user-api-key]:[current minute number]"  and value will be count. 

There will be 3 steps in the process:- 
1. We'll use command: GET [user-api-key]:[current minute number], if result is less than limit (say, 10) we will proceed to step 3. Otherwise we'll move towards step 2.
2. As result of 1. is greater than limit, we'll throw an error message.
3. As result of 1. is less than limit, we'll increment the count for the key "[user-api-key]:[current minute number]" and set timeout for the current key.

