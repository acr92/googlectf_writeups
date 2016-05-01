# Opabina Regalis SSL Stripping

## Challenge

Following on from Opabina Regalis - Fetch Token, can you implement an SSL stripping attack?

## Solution

I just sent a few messages back and forth to get a feeling of the content. I saw that we
got a large HTML page back, and I decided to save that and open it in Firefox.

From there I saw a URL to `/user/sign_in`.

Then I modified the request to GET `/user/sign_in` instead of GET `/`, and I got the flag.

*Token is*: `CTF{Why=were=the=apple=and=the=orange=all=alone..Because=the=banana=spli7}`
