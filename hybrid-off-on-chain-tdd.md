# Designing a Hybrid Zero-Knowledge Proof System for Ethereum Address Ownership Verification

## Overview

This document presents a solution designed to enable private, safe, and partially trustless verification of Ethereum address ownership leveraging zero-knowledge proofs (ZKPs). Given the challenge posed by the large size of proofs, which makes on-chain verification impractical, the proposed solution combines client-side proof generation with off-chain verification and on-chain storage of verification metadata.

## Context

The current AnonKlub system utilizes client-side generated ZKPs, ensuring privacy by concealing the specifics of the proof generation process, especially the address. A critical aspect of the design involves integrating mechanisms to prevent proof reuse (via nullifiers) and facilitate transparent verification despite the impracticality of on-chain proof verification due to proof size constraints (spartan proofs are ~15KB).

## Goal

To develop a mechanism allowing users to anonymously prove ownership of Ethereum addresses that is private, ensures the safety of proofs against reuse, and enhances trust through transparency in verification, within the given constraints.

## Solution Overview

### Key Components

- **Client-Side Proving System**: Users generate ZKPs on their devices, with the computation outputting both the proof and a unique nullifier, ensuring the privacy and uniqueness of each proof.
- **Single Verifying Entity**: Assumes the role of verifying proofs off-chain. This design choice introduces a trust assumption but is tolerated given the current technological constraints.
- **Smart Contract for Metadata Storage**: A smart contract records nullifiers and IPFS links to proof data on the Ethereum blockchain, enhancing transparency and verifiability by preventing proof reuse.

### Implementation Details

1. **Proof Generation and Nullifier Output**: In the client-side proving step, users generate ZKPs that include the necessary data for proving Ethereum address ownership. Importantly, this step also generates a unique nullifier for each proof, integral to preventing proof reuse.

2. **Off-Chain Verification**: The single verifier entity checks the proofs off-chain, verifying their validity based on the provided data and the uniqueness of the nullifier.

3. **On-Chain Storage**: Upon successful verification, the nullifier and an IPFS link to the detailed proof data are recorded in a smart contract on the Ethereum blockchain. This process ensures that each proof can be independently verified and is not reused, while also making the verification process transparent.

## Trust Considerations

The reliance on a single verifying entity introduces a centralized trust assumption in their capability and integrity. However, the public recording of nullifiers and proof data links on the blockchain enhances the system's transparency, partially mitigating this trust concern.

## Potential Enhancements

### Decentralized Verification Network

Future enhancements could include transitioning to a decentralized network of verifiers to eliminate the centralized trust assumption. This network would independently verify proofs, potentially leveraging consensus mechanisms for added security and trustlessness.

### Data Availability Solutions

To circumvent the limitations of large proof sizes, exploring blockchain platforms focused on data availability and storage might offer a solution (Celestia, Arweave ...).


## Conclusion

The described solution offers a practical approach to achieving private, safe, and transparent verification of Ethereum address ownership. It acknowledges the current limitations in achieving full trustlessness due to the reliance on a single verifying entity and proposes future pathways to enhance decentralization and trustlessness in the system.
