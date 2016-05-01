# Opabina Regalis Input Validation

## Challenge

Following on from Opabina Regalis - Fetch Token and Opabina Regalis - 
Downgrade Attack - can you find an input validation request that would 
allow you to access otherwise protected resources?

## Solution

For this I just re-used all the code from Opabina Regalis Downgrade Attack.

I just had to change the URI to point to `/protected/token` instead of
`/protected/secret`, and it was done.

*Token is:* `CTF{-Why-dont-eggs-tell-jokes...Theyd-crack-each-other-up-}`
