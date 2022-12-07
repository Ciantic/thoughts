# Learning Mastodon's ActivityPub API with CURL and JQ

I pipe all outputs to JQ for better viewing experience

```bash
#!/bin/bash

# Get Gargron@mastodon.social
# This is not part of ActivityPub, but rather an extension to Mastodon
#
# In ActivityPub there is no handles, each user ID is an URL, which we get from the alias in a webfinger:
curl "https://mastodon.social/.well-known/webfinger?resource=acct:Gargron@mastodon.social" | jq

# Notice the aliases property, which contains the ActivityPub ID's
# "aliases": [
#    "https://mastodon.social/@Gargron",
#    "https://mastodon.social/users/Gargron"
#  ],

# According to spec the headers need to be following for each query to ActivityPub endpoints:

HEADERS='Accept: application/ld+json; profile="https://www.w3.org/ns/activitystreams"'

# Then query ActivityPub profile from that alias:
curl -H "$HEADERS" "https://mastodon.social/users/Gargron" | jq

# In above, notice the ID property:
# "id": "https://mastodon.social/users/Gargron",
# That URL is the canonical ActivityPub ID for Gargron
# That means that if you want to follow Gargron, you need to follow that URL, similarily list of followers are list of these ActivityPub ID's.

# Get latest public posts
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/outbox" | jq

# Get first page of public posts
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/outbox?page=1" | jq

# Follower count
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/followers" | jq

# Follower list (may fail if hidden by user)
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/followers?page=1" | jq
```

[Read the ActivityPub spec](https://www.w3.org/TR/activitypub/)
