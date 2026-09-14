# mf-nodeops-comms
Repository containing GPG public keys associated with the Monad Foundation, node operators announcements and their associated GPG signatures

## How it works
The Monad Foundation announcements to node operators will be GPG signed. Once the Monad Foundation sends a message via official node operators channels (Discord, Email, Slack, Telegram), node operators can independently verify the authenticity of the message by verifying the GPG signatures. Each message will contain:
- `announcement.txt`  - the readable announcement ([example](announcements/mf-0/announcement.txt))
- `announcement.sig`  - the combined signatures from 2+ authorized signers ([example](announcements/mf-0/announcement.sig))
The readable announcement will contain:
- an unique index (e.g. MF Announcement #0)
- an UTC creation timestamp in the ISO 8601 format (e.g. Created: 2026-08-08T08:08:08Z)
- the actual message content
The signature file will contain the combined PGP signatures from 2+ authorized signers.

The messages will be sent/posted after the creation timestamp, the index will be incremental and each message will include signatures from at least two authorized signers. Their public keys can be found in the official [repository](https://github.com/monad-crypto/mf-nodeops-comms/tree/main/keys), while their full primary-key fingerprints can be found in the official [documentation](https://docs.monad.xyz/node-ops/gpg-keys.json).

## How to verify the signature
- Install GPG (different based on platform, check the official website [here](https://www.gnupg.org/download/))
- Clone the repository
```
# Skip this step if you have already cloned the repository
git clone https://github.com/monad-crypto/mf-nodeops-comms.git
# Pull the latest changes
git pull
```
- Confirm the displayed fingerprints match the authorized Monad signing-key fingerprints published [here](https://docs.monad.xyz/node-ops/gpg-keys.json) before importing them
```
cd mf-nodeops-comms
gpg --show-keys --with-fingerprint keys/*.pub.asc
```
- Import keyring
```
gpg --import keys/*.pub.asc
```
- Verify message for signatures
```
# This is an example announcement
gpg --verify announcements/mf-0/announcement.sig announcements/mf-0/announcement.txt
```
Example output:
```
gpg: Signature made Wed Sep  9 17:11:20 2026 EEST
gpg:                using EDDSA key B26F10A7157EA66528FD21381CD1328B3352B251
gpg: Good signature from "signer_1" [unknown]
gpg: Signature made Wed Sep  9 17:16:06 2026 EEST
gpg:                using EDDSA key 53E38FB05A545B69C2C284EA27C4446634EC4967
gpg: Good signature from "signer_3" [unknown]
gpg: ...
```

Attention: GPG may warn that a key is “not certified with a trusted signature.” This is expected when the imported key has not been locally trusted. Confirm that the primary key fingerprint matches the authorized fingerprint published in the official Monad documentation before accepting the signature.
