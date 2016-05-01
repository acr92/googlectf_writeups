# Opabina Regalis Downgrade Attack

## Challenge
Following on from Opabina Regalis - Token Fetch, this challenge listens on ssl-added-and-removed-here.ctfcompetition.com:20691.

## Solution

The client makes a request to the server to `/protected/not-secret`. We want to modify that to `/protected/secret`.

We get a reply from the server, where it gives us [HTTP Digest](https://en.wikipedia.org/wiki/Digest_access_authentication)
information, and the client is expected to reply correctly to this.

The name of the challenge provides us with a hint that we need to downgrade the request, so we simply modify the reply
from the server to reply with `Basic realm="In the realm of hackers"` instead of the proper `Digest ...` message.
We then downgrade it from HTTP Digest authentication, to HTTP basic authentication.

When we do this, we get back a message with the header: `Basic Z29vZ2xlLmN0ZjoxOTQ0MTU1NjgyLjY2NzgzNzcxNC4yMTE5MjUyMTk0`

HTTP Basic authentication just uses `base64({username}:{password})` so we simply run base64 decode on the string, split
it into the `username` and `password`, and store that for use later.

The next part is then to generate the proper message that we should send to the server to get our token. We need to
send this message using HTTP Digest authentication, since that's what the server expects.

To do this, we need to extract some information from the reply made earlier. From this message:

```
Digest realm=\"In the realm of hackers\",qop=\"auth\",nonce=\"72b8a80341ce2885\",opaque=\"72b8a80341ce2885\"
```

We need to extract the `nonce` and `opaque` value. We will use this in a minute.

To generate a HTTP Digest response, we need `username`, `realm`, `password`, `method`, `uri`, `nonce`, `nc` and `cnonce`.
Since `nc` and `cnonce` is chosen by us, they can be anything. `uri` we know to be `/protected/secret` so we
just hardcode it to that. The rest of the variables we've obtained throughout the packets, and we're now ready
to generate the response.

We override the request packet (the one we got earlier with Basic authentication info) to point to `/protected/secret` and
we generate a proper response. We then forward all of this to the server, and read the reply.

This should provide you with the token.

*Token is:* `CTF{What:is:green:and:goes:to:summer:camp...A:brussel:scout}`
