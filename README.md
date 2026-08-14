# mf-nodeops-comms-keyring
Repository containing GPG public keys associated with the Monad Foundation

## How it works
The Monad Foundation announcements to node operators will be GPG signed. Once the Monad Foundation sends a GPG-signed message via official node operators channels (Discord, Email, Slack, Telegram), node operators can independently verify the authenticity of the message by verifying the GPG signatures. All GPG-signed messages will contain:
- an unique index (e.g. MF Announcement #0)
- a creation timestamp (e.g. Created: 2026-08-08T08:08:08)
- an expiration timestamp (e.g. Expires: 2026-09-09T09:09:09)
- the actual message content
- a PGP signature

The messages will be sent/posted between the creation timestamp and the expiration timestamp, the index will be incremental and each message will include signatures from at least two authorized signers whose public keys can be found in the [keys folder](keys/).

## How to verify the signature
- Install GPG (different based on platform, check the official website [here](https://www.gnupg.org/download/))
- Clone the repository
```
git clone https://github.com/monad-crypto/mf-nodeops-comms-keyring.git
```
- Import keyring
```
gpg --import keys/*.pub.asc
```
- Verify message for signatures
```
gpg --verify example_release.signed.asc
```
Example output:
```
gpg: Signature made ...
gpg:                using EDDSA key ...
gpg: Good signature from "signer_x" ...
gpg: Signature made ...
gpg:                using EDDSA key ...
gpg: Good signature from "signer_y" ...
gpg: ...
```

Attention: there might be some warnings such as `This key is not certified with a trusted signature!` or `There is no indication that the signature belongs to the owner.` and they can be safely ignored.
