# Mastodon has identity problem

I have been testing Mastodon but I find the idea that your account is tied to an instance old school centralization. This makes Mastodon much harder to use as Twitter replacement.

Just browsing instances, you find a lot of which has set of rules which ban certain type of content. Uusually for good reason, but some are trying to curate the local timelines as if the whole instance is topical.

In my opinion topical instances are a great idea. Naturally a community who knows a lot about astronomy are better at moderating astronomy content, e.g. astrodon.social. However fediverse isn't suited for topical instances as one can't post from one instance to another. All posts you post are going to server your account is in, thus you are stuck with moderation guidelines of your server.

For example if you want to post political content and astronomy related content, to do that now you need _two_ accounts, one for astrodon.social and another to political instance. Unless you think your content is suitable for both.

It would be easier if one could have single account for whole fediverse and be able to post to any instance. We have the tools to do that, but I don't know can Mastodon/ActivityPub be bent to that. It would require to separating the accounts from instances.

## Naive idea: Private/public key pair as an account identifier

One solution would be to have private / public key as account. Then to post you'd have some sort of EdDSA signed payload like JSON object that describes who you are and url to your profile picture.

When you post to new server it would send your public key, signed profile JSON and then you could start posting to a server.

However this too has a one problem, what happens if you loose your private key? It will happen and then you'd loose whole account. This means identifier must be something that user can reset without help of the servers.

## Distillied idea: URL to your profile as an account identifier

Identifier needs to be in a place you control so that you can reset the private key. Domains are usually well guarded entities in internet, if you loose your domain you loose your brand. For this reason URL is pretty good account identifier.

Profile _URL_ should contain your profile file, with your name, profile image url and your public key. For example, John Doe has an account with identifier: `https://example.com/john.txt`

In john.txt it contains something like:

```jsonc
[
    // First object is current profile
    {
        "name": "John Doe",
        "picture": "https://example.com/john.jpg",
        "valid_from": "2022-11-19 12:00:00",
        "public_key_ed25519": "MTIzNDU2Nzg5MDEyMzQ1Njc4OTAxMjM0NTY3ODkwMTI=",

        // Signature of this JSON object (without the signature):
        "eddsa_signature": "Nzg5MDEyU2Nzg5MDY3O..."
    },

    // Old profiles, which are not to be used to sign messages anymore...
    {
        "name": "John Doe",
        "picture": "https://example.com/john.jpg",
        "url": "https://example.com/john.txt",
        "valid_from": "2021-01-01 12:00:00",
        "public_key_ed25519": "5MDEyMzQ1Njc4OTAxMjM0NTY3ODMTIzNDU2NzgkwMTI=",
        "eddsa_signature": "zg5MDNzg5MDEyU2NY3O..."
    }
    // ...
]
```

Client server communication would be something like this:

-   When John posts to a server he uses URL has identifier
-   Server reads the URL, if it's not found, it creates John on their server with given public key
-   All messages John posts need to be signed with valid public key in the account URL

This idea is rather raw at the moment, but the gist of it is above. There are issues that needs to be resolved, like if you want to move your identity file to different URL, it needs redirect 302 and maybe a field.

All likes, posts, boosts, followers etc. would be still stored in instance servers, but individuals would be identified by URL to their profile.
