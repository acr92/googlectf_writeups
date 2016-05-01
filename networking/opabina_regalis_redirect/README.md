# Opabina Regalis - Redirect

## Challenge

Following on from Opabina Regalis - Token Fetch, can you get access to the `/protected/secret` URI?

## Solution

When we get the 401 Unauthorized reply from the server, instead of forwarding that, we modify it to a
`302 REDIRECT`, add a `Location` header pointing to `/protected/secret`, send a few messages back
and forth until finally we get the token.

*Token is:* `CTF{Why,do,fungi,have,to,pay,double,bus,fares----because,they,take,up,7oo,Mushroom}`
