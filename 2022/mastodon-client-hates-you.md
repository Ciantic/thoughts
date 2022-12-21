# Mastodon's web client hates you

This is work in progress.

This is a bit of a rant, but it's because I want Mastodon to succeed, but right now its web client is so bad that it feels like it's fighting against the user.

-   Defaulting to a dark theme is driving people away.
-   Following people is difficult.
    -   Showing full details of all mentioned people in toot is not there.
    -   Too much copy pasting
-   Showing old toots is difficult.
-   Showing a full list of followers is difficult.
-   Showing another server's home timeline is difficult.
-   Settings are all over, and some of them are not found in the preferences.
-   Featured tags are listed in the bottom right corner of the UI, undiscoverable.
-   People search doesn't index hashtags.
-   The user interface has colors that make it unclear what is a field.
-   Lists are unintuitive to use, and slow, it also uses bad color for the search field.

All of these could have been fixed.

A lot of these foot guns come from ActivityPub, it can't sign messages sitting in an outbox, thus forwarding something like a follower list or older toots is not "safe" it can lie to you.

It's amazing that ActivityPub which is a decentralized protocol is not based on signed messages, this problem was solved a long time ago: GPG, remember that?

The only thing Mastodon/ActivityPub signs are HTTP signatures, but since these aren't stored alongside messages they are useless. It should sign messages itself and store them with messages.
