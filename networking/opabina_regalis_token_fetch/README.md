# Opabina Regalis Token Fetch

## Challenge
There are a variety of client side machines that have access to certain websites we'd like to access. We have a system in place, called "Opabina Regalis" where we can intercept and modify HTTP requests on the fly. Can you implement some attacks to gain access to those websites?

Opabina Regalis makes use of Protocol Buffers to send a short snippet of the HTTP request for modification.

## Solution

The real challenge here is just getting protocol buffers running, and understanding how it works.

I copied the protocol buffer definition provided into `format.proto`, ran:

```
protoc -I=. --python_out=. format.proto
```

and got the definition.

Then I created a simple framework, which I re-used for the next opabina regalis challenges.

The second part of the challenge is understanding what the task actually is...We're a
Man-in-the-middle proxy between requests, and we can modify the requests however we'd like.

We simply change the `i.request.uri` from `/not-token` to `/token`, forward that to the server,
and read the reply back.

*Token is:* `CTF{WhyDidTheTomatoBlush...ItSawTheSaladDressing}`
