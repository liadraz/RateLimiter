
# Rate Limiter Assignment

## Motivation 
Rate limiters are mechanisem that limit the number of requests that can be made to a specific endpoint.

## Requirements

- Initialize with a Function (Func<TArg, Task>) and several rate limits. (Pool of rate limits?)
- Provide an action method **Perform**, `Task Perform(TArg argument)`
- Support multiple running rate limits ensuring all are respected.
- Delays exection when necessary to comply with rate limits.
- Handles concurrent calls from multiple threads safely. 
    e.g A passed function might be a call to external API, and it should receive the rate limits
        10 per second, 100 per minute, 1000 per daytime
- Support multiple rate limits simultaneously. 

> *NOTE Do not use external Libraries*

## Implementation Approaches

### Sliding Window
Ensure that you are limited to 10 requests in any rolling 24-hour window.

*Pros*
- Prevents bursts near the reset times
- Less restricts clients to specific time (a human user / bot)
- Requests are more scattered during the day and flexiable to the 
user.

*Cons*
- Complex implementation
- Uses more memory to track all timestamps.
- Handles timestamps for each execution.

#### Absolute
Ensure 10 requests are made on a calendar day starting at midnight (00:00).

*Pros*
- Predictable
- Easy to implement
*Cons*
- Can exceed the limit in a very short time or near reset times.

## How To Test It

## Usage

---

## *AsIs*
`Create a RateLimiter in C#.
It's purpose is to be initialized with some Func> and multiple(!) rate limits.

It is then called like so:
Task Perform(TArg argument) to perform the action. 
 
It guarantees that ALL rate limits it holds are honored, and delays execution until it can honor > the rate limits if needed. 
 
The RateLimiter IS expected to be called from multiple threads at the same time - you must > accommodate that. For example, the passed function might be a call to some external API, and it may> receive the rate limits: 10 per second, 100 per minute, 1000 per day
 
There are two approaches to Rate Limiting. Let's imagine a single RateLimit of 10 per day. The > approaches are:
1. Sliding window - Where the RateLimiter ensures that no more than 10 were executed in the last24 > hrs, even if the call is made in the middle of day
2. Absolute - Where the RateLimiter ensures that no more than 10 were executed THIS day, that is,> since 00:00.You need to choose the approach to implement, and explain why (pros / cons), and then> implement the RateLimiter.
 
Do not use or consult external libraries - YOU need to implement this.`