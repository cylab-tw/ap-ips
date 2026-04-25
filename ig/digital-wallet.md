# Digital Wallet - Asia-Pacific Patient Summary v0.1.0

* [**Table of Contents**](toc.md)
* **Digital Wallet**

## Digital Wallet

# Digital Wallet

Asia-Pacific Patient Summary supports a digital health wallet model where a patient can carry and present IPS data as verifiable credentials.

## Design Goals

* Portable cross-border patient summary access
* Cryptographic trust using signed credentials
* Privacy with selective disclosure (for example SD-JWT)
* Support for online and offline presentation flows

## Exchange Pattern

1. Issuer prepares IPS-based credential
1. Patient wallet stores credential
1. Verifier requests selected content with patient consent
1. Verifier validates signature and uses disclosed data for care

![](track3-wallet.jpg)

