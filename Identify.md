# Identity

## Overview

The Shog protocol implements its identity system using ECDSA.

## Identity Structure

- Unique identifier
- Name
- Guardian email hash
- Signature public key identifier
- A set of Identity key-value pairs

This structure makes up the Shog Id

### Unique Identifier
The Shog ID is generated using ECDSA public key and creation timestamp, similar to Base58check:

Calculate the keccak256 hash of a secp256k1 public key concatenated with the current Unix timestamp (in seconds), and take the last 20 bytes

### Name

Each Identity can have a unique Name
If an Identity shows no activity for one year, its Name becomes available for use by other Identities

### Guardian Email

DKIM verification is used to verify emails from the guardian address
Guardian email is used for verification when signing keys need to be renewed or changed
It's also used for signature key verification

### Signature Public Key Identifier

Calculate SHA256 hash of the signature public key and take the last 20 bytes

### Identity Key-Value Pairs

Can be used for custom Identity attributes and properties
