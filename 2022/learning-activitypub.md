# Learning Mastodon and ActivityPub API with CURL and JQ

I pipe all outputs to JQ for a better viewing experience

```bash
#!/bin/bash

# 1. Get Gargron@mastodon.social, and from there get the ActivityPub IDs
curl "https://mastodon.social/.well-known/webfinger?resource=acct:Gargron@mastodon.social" | jq

# Headers for ActivityPub queries
HEADERS='Accept: application/ld+json; profile="https://www.w3.org/ns/activitystreams"'

# 2. Then query ActivityPub profile from that `activity+json` link:
curl -H "$HEADERS" "https://mastodon.social/users/Gargron" | jq

# Get latest public posts collection
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/outbox" | jq

# Get first page of public posts
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/outbox?page=1" | jq

# Follower collection with count
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/followers" | jq

# Follower list (may fail if hidden by user)
curl -H "$HEADERS" "https://mastodon.social/users/Gargron/followers?page=1" | jq
```

Notice, that you cannot send messages to other people because it requires signed HTTP signatures. To post messages to other people's inboxes, you would need your account's private key which is stored in the Mastodon instance's server.

## Notes

1. Get `Gargron@mastodon.social`'s webfinger. This is not part of ActivityPub, but rather an extension of Mastodon. Notice the `links` property contains an array, one of which contains the ActivityPub ID:
    ```
    {
      "rel": "self",
      "type": "application/activity+json",
      "href": "https://mastodon.social/users/Gargron"
    },
    ```
2. Query ActivityPub profile URL, notice in the profile property ID, which is the same as the one in the Webfinger:
    ```
    {
        "id" : "https://mastodon.social/users/Gargron",
    }
    ```

-   [Read the ActivityPub spec](https://www.w3.org/TR/activitypub/)
