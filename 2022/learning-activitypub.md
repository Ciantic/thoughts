# Learning Mastodon's ActivityPub API with CURL and JQ

I pipe all outputs to JQ for better viewing experience

```bash
#!/bin/bash

# 1. Get Gargron@mastodon.social, and from there get the ActivityPub IDs
curl "https://mastodon.social/.well-known/webfinger?resource=acct:Gargron@mastodon.social" | jq

# Headers for ActivityPub queries
HEADERS='Accept: application/ld+json; profile="https://www.w3.org/ns/activitystreams"'

# 2. Then query ActivityPub profile from that alias:
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

## Notes

1. Get `Gargron@mastodon.social`'s webfinger. This is not part of ActivityPub, but rather an extension to Mastodon. Notice the `aliases` property, which contains the ActivityPub ID's:
    ```
    {
        "aliases": [
            "https://mastodon.social/@Gargron",
            "https://mastodon.social/users/Gargron"
        ]
    }
    ```
2. Query ActivityPub profile URL, notice in the profile property ID, which is the same as the one in the webfinger:
    ```
    {
        "id" : "https://mastodon.social/users/Gargron",
    }
    ```

-   [Read the ActivityPub spec](https://www.w3.org/TR/activitypub/)
