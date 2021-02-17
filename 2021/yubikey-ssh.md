#  Logging to SSH servers with YubiKey

Steps are roughly:

*   Create GPG identity, if you don't have already
*   Move subkeys to YubiKey
*   Use GPG's ssh-agent

Pre-requisites:

*   GnuPG or GPG4Win
*   YubiKey or equivalent smart card

## Creating GPG identity for yourself

GPG uses public key cryptography to proof your identity, encrypt and decrypt data, sign messages, and authenticate to external services. These are enabled by having main master key and subkeys with different capabilites based on the use cases.

Master key makes your GPG identity which always has capability called `certify`, this capability allows to mint new keys and revoke keys. You could give this capability to subkey also, but it's probably not wise. This key should be kept in very secure place. Preferably use this key only from offline computer in your closet full of spider web. For similar reasons you should have a good backup for this key. Consider creating a paper backup or qr code. Note that each backup is still protected by your passphrase so it should not need extra encryption.

Subkeys are additional keys with other capabilities: `sign`, `encrypt`, or `authenticate`. You can choose to create as many subkeys as you want. For instance it's pretty common to have multiple authentication keys if you have multiple smart cards. You could also copy same authentication key to multiple keys, as I intend to do, because changing SSH public keys are pain. However if you loose the authentication key, then you need to revoke it. Since SSH servers don't have automatic revoke system you must login to all servers and remove your public key.

If you want to encrypt files or sign messages, you should create separate keys for these actions. Combining encrypt capability along with other capabilities is not wise because of legal reasons. Some jurisdictions may compell you to give the encryption keys, and if you have combined your encrypt key with your authentication key, you are toasted. Now you are required by law to hand over your authentication key in the process.

GPG provides multiple crypotgraphic algorithms, for instance RSA 4096bit, ed25519, etc. Choosing between these without expertise in the cryptography is futile effort. Luckily the choice is made easier if you trust the [GPG Esoteric Options page](https://www.gnupg.org/documentation/manuals/gnupg-devel/GPG-Esoteric-Options.html), it says that "future default" algorithms are ed25519 for sign / certify, and cv25519 for encryption. I guess they aren't defaults yet because older GPG versions don't understand them. Note that the ed25519 was added to OpenSSH version 6.5 in January 2014. If you run old rigs you can't use it to authenticate to your SSH server, in that case use RSA for authentication.

Let's start by creating your identity. Log in to secure environment (offline Raspberry Pi in your closet / live CD / choose anything by your level of paranoia) with gpg(2) installed, and start creating your GPG identity:

```bash
# Ephemeral and empty GNU PGP directory, allowing you to try several times
export GNUPGHOME=$(mktemp -d)

# --list-keys first to ensure you are not editing existing GPG entries
gpg --list-keys 

# Give very secure passphrase because this is inteded to secure your minting key, 
# the one you keep in your closet, out of sight. It is also used to secure the paper 
# backup if you happen to create one.
gpg --quick-generate-key "John Doe <john.doe@example.com>" ed25519 cert never
FPR=$(gpg --list-options show-only-fpr-mbox --list-secret-keys | head -1 | cut -d' ' -f1)

# Add more identities
# 
# gpg --quick-add-uid $FPR "John Doe <john@example.com>"
# 
# Then manually add trust to the identification: 
# gpg --edit-key $FPR
# gpg> trust
# gpg> 5
# gpg> save

# Subkeys for your YubiKey
gpg --quick-add-key $FPR ed25519 sign never
gpg --quick-add-key $FPR ed25519 auth never
gpg --quick-add-key $FPR cv25519 encrypt never
```

For testing, you may pass empty passphrase and avoid interactivity by giving: `--no-tty --batch --passphrase ''` to `gpg` commands.

## Exporting and backing up your keys

You should export your secret keys and public keys. Secret keys you store for backup purposes, note that the exported secret keys file includes the public keys, so for strictly backup purposes you don't need to store the public keys file. However you need public keys as well because they are required on your daily machine since the YubiKey does not have means to fetch them.

```bash
gpg --output keys.key --armor --export-secret-keys $FPR # A backup of everything
gpg --output keys.pub --armor --export $FPR # A public keys which you copy to your daily machine

# -- Copy `keys.pub` to a memory stick and carry it to your daily machine --
```

## Moving subkeys to YubiKey

GPG has command `keytocard` but it is *destructive*, it removes the key from your GPG directory. You need to have a backup in case you want to keep minting more YubiKeys with same subkeys. You could have different subkeys for different YubiKeys, but it may become maintenance problem as then you have multiple SSH public keys and multiple encryption keys (which GPG doesn't even support, see notes at the end).

Changing the passphrase may be wise as the one you gave during the identity creation is intended to secure the *backup* or the *server in the closet* which is accessed very seldomly, so do not use the same passphrase for daily subkeys. However with YubiKey the passphrase is replaced by the pin, so changing the passphrase is not strictly necessary because it's overwritten anyway.

```bash
# Start with a fresh GPG directory, and import your secret keys from a backup you just made
export GNUPGHOME=$(mktemp -d)
gpg --import keys.key
gpg --list-keys --with-subkey-fingerprints
FPR=$(gpg --list-options show-only-fpr-mbox --list-secret-keys | head -1 | cut -d' ' -f1)
gpg --edit-key $FPR

# Change passphrase, because these subkeys are for daily usage
gpg> passwd

# Select subkeys, and move to card
# YubiKey default Admin PIN 123456
gpg> list
gpg> key 1
gpg> keytocard
gpg> key 2
gpg> keytocard
gpg> key 3
gpg> keytocard

gpg> save

# Change YubiKey's OpenPGP PIN and OpenPGP Admin PIN
gpg --change-pin
```

OpenPGP PIN is required each time the YubiKey boots up and you start to use the GPG. The OpenPGP Admin PIN is required if you want to change keys on the YubiKey.

## Create SSH public key for servers

The `authentication` subkey allows to generate an ssh public key

```bash
# If you have only *one* authentication subkey, you can get it's SSH public key:
gpg --export-ssh-key $FPR

# If you have multiple authentication subkeys, you must specify the subkey fingerprint:
gpg --list-keys --with-subkey-fingerprints
gpg --export-ssh-key SUBKEYFPR! # Notice (!) is required, otherwise it will give you only the latest
```

## On your daily terminal

Plug in your YubiKey, and copy the public keys for importing. 

```bash
# Ensure you are working on empty GPG installation:
gpg --list-keys 

# Import public keys and connect them to YubiKey
gpg --import keys.pub
gpg --card-edit
gpg> fetch
gpg> quit

ykman openpgp
```

## Setup SSH to use OpenPGP

Add following to your `.bashrc`, or for example `/etc/profile.d/ssh-pgp-agent.sh`:

```bash
export SSH_AUTH_SOCK=$(gpgconf --list-dirs agent-ssh-socket)
gpgconf --launch gpg-agent
```

For Windows GPG4Win it's enough to edit `gpg-agent.conf` and add this line:

```
enable-putty-support
```

TODO: Add WSL2 script instructions.

## Other notes

*   You can inspect many details about the exported secret keys, public keys and ecrypted files with `--list-packets`.  I recommend running it between key creations and other actions to try to understand what the files contain or how they change. E.g. to inspect public key (`gpg --armor --export | gpg --list-packets`), or to inspect encrypted data (`echo "foo" | gpg --armor --recipient $FPR --encrypt | gpg --list-packets`).

*   To export just specific subkeys, you need to first get the subkey fingerprints, and then specify which subkey you want to export:

    ```bash
    gpg --list-keys --with-subkey-fingerprints
    gpg --output subkey.key --armor --export-secret-keys SUBKEYFPR! # Exclamation (!) at the end is required
    ```

*   GnuPGP uses only the latest valid subkey with `encrypt` capability for encryption. There is no way to decrypt with specified subkey without actually removing other keys. 

*   You can extract public key of individual subkeys using `gpgsplit` for instance `gpg --export | gpgsplit`, it creates multiple files. If you want to export a specific public key, you can do `gpg --export SUBKEYID! | gpgsplit`.

*   It's possible to convert ASCII armored back to binary using `cat armored.txt | gpg --dearmor > armored.bin`. This is required if you use gpgsplit as otherwise it just gives unhelpful error `invalid CTB 2d`.

*   It's possible to create subkeys with no capabilities at all, I think those [could be stored on YubiKey if you use PIV feature](https://developers.yubico.com/PIV/Guides/SSH_with_PIV_and_PKCS11.html). With YubiKey's OpenPGP mode you can't store arbitrary keys, only keys with specific capabilities.

*   Adding or changing any key or UID changes also your public key (`gpg --armor --export`) as well as your signature. People communicating with you should update the public keys accordingly. *Note:* GPG changes does not change your SSH public key, which always points to the latest `auth` subkey.

*   If you export secret keys (`gpg --armor --export-secret-keys`) the public key can be derived from the private key, even though it says only `BEGIN PGP PRIVATE KEY BLOCK`.