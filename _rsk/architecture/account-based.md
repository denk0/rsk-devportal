---
title: Account Based RSK Addresses
tags: rsk, checksum, chainId, address, derivation, eip1191, eip155, bip44, slip44
description: "EIP-1191 chainId is used in RSK addresses as a checksum. m/44'/137'/0'/0 is the derivation path used for BIP-44 compatible wallets."
collection_order: 3
menu_title: Account Based
menu_order: 2
---

RSK Addresses incorporate an optional blockchain identifier (also known as `chainId`). If the `chainId` is not present, it is assumed the address refers to the RSK main network.

## How to get an address

Check out the already [integrated wallets](/develop/apps/wallets) or [integrate your wallet](/develop/apps/integrate).

## Derivation path info

When using
[BIP-44](https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki "Multi-Account Hierarchy for Deterministic Wallets")-compatible
wallet software, you will need to specify a derivation path.

```
RSK Mainnet: m/44'/137'/0'/0/N
RSK Testnet: m/44'/37310'/0'/0/N
```

- The first level of the hierarchy is for *purpose*.
  This is always `44'`, as per the BIP44 specification.
- The second level of the hierarchy is for the *registered coin type*.
  - For RSK Mainnet, this should be `137'`, as per the
    [SLIP-44](https://github.com/satoshilabs/slips/blob/master/slip-0044.md "Registered coin types for BIP-0044")
    specification.
  - For RSK Testnet, this should be `37310'`, as per the
    [RSKIP-57](https://github.com/rsksmart/RSKIPs/blob/master/IPs/RSKIP57.md "Derivation Path for Hierarchical Deterministic Wallets")
    specification.
- The final level of the hierarchy is for *index*: Addresses are numbered from index 0 in sequentially increasing manner. This number is used as child index in [BIP32 derivation](https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki#specification-key-derivation "Hierarchical Deterministic Wallets - Key Derivation"). Public derivation is used at this level.

## Checksum

RSK implements [EIP-1191](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1191.md) to protect users from losing funds by mixing addresses of different Ethereum based networks.

[In this document](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1191.md), you can find out how to apply the checksum and validate an address. This EIP is also supported by Web3 and hardware wallets.

## ChainId

To avoid a replay attack by using an already-signed transaction, originally broadcast in “network A”, and subsequently replayed it in “network B”, the EVM-based networks use `chainId` as part of the transaction properties.
All `chainId`s can be found at [chainid.network](https://chainid.network/).

```
RSK Mainnet: 30
RSK Testnet: 31
```

See [EIP-155](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-155.md#user-content-list-of-chain-ids) for more information.

We strongly recommend the following:

1. Add the `chainId` in the RSK integration (and every time you integrate EVM-based blockchains)
2. Use a different account to hold value for each blockchain (do not share the same account among RSK, ETH, and others)
