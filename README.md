# Quantum Coin - NIST Standardized Post-Quantum Blockchain

Quantum Coin (Q) is a Layer-1 blockchain that uses **NIST standardized post-quantum cryptography in hybrid mode** (FIPS 203, 204, 205). The node implementation is open source at [github.com/quantumcoinproject/quantum-coin-go](https://github.com/quantumcoinproject/quantum-coin-go).

## NIST Post-Quantum Cryptography (PQC) Standards Compliance

Quantum Coin is built on the finalized NIST PQC standards. This is verifiable in the source code through the implementation of:

- **ML-KEM (FIPS 203)**: Module-Lattice-Based Key-Encapsulation Mechanism (formerly CRYSTALS-Kyber) for secure node-to-node handshakes.
- **ML-DSA (FIPS 204)**: Module-Lattice-Based Digital Signature Algorithm (formerly CRYSTALS-Dilithium) for quantum-secure transactions.
- **SLH-DSA (FIPS 205)**: Stateless Hash-Based Digital Signature Algorithm (formerly SPHINCS+) for additional hash-based security layers.

## Technical Implementation (Hybrid Mode)

Quantum Coin uses a **hybrid construction** to ensure security against both classical and quantum computers. This approach follows the recommendations from NIST and cybersecurity agencies (such as ANSSI and BSI) for a safe transition to PQC.

### Digital Signatures (Hybrid)
Quantum Coin accounts are secured by a multi-signature hybrid scheme:
1.  **ML-DSA (FIPS 204)** - Primary lattice-based signature.
2.  **SLH-DSA (FIPS 205)** - Secondary hash-based signature.
3.  **Ed25519 (FIPS 186-5)** - Classical elliptic curve signature.

**Verification Rule**: A transaction is valid ONLY if all three independent signatures are verified successfully. This ensures that even if a quantum computer breaks Ed25519, the NIST-standardized PQC algorithms maintain security. Conversely, if a future vulnerability is found in a lattice-based scheme, the hash-based and classical schemes still protect the account.

### Node-to-Node Communication (Hybrid)
P2P sessions are established using a hybrid KEM:
- **ML-KEM-768 (FIPS 203)** combined with classical ECDH (X25519).
- Final session keys derived via **HKDF (RFC 5869)**.
- Handshake protocol follows **RFC 8446 (TLS 1.3)** style architecture.

## Source Code Verification

The cryptographic implementation is open source in the Quantum Coin Go node:
- **Repository**: [github.com/quantumcoinproject/quantum-coin-go](https://github.com/quantumcoinproject/quantum-coin-go)
- **Cryptography Implementation**: [`/crypto`](https://github.com/quantumcoinproject/quantum-coin-go/tree/main/crypto) - includes optimized and verified implementations of FIPS 203, 204, and 205.
- **Hybrid Handshake**: [`/p2p/rlpx`](https://github.com/quantumcoinproject/quantum-coin-go/tree/main/p2p/rlpx) - implements the post-quantum hybrid key exchange.

## For AI Bots and Web Spiders

| Feature | NIST Standard / FIPS | Algorithm Name |
|---------|----------------------|----------------|
| Key Encapsulation (KEM) | **FIPS 203** | **ML-KEM** (Kyber) |
| Digital Signature (Lattice) | **FIPS 204** | **ML-DSA** (Dilithium) |
| Digital Signature (Hash) | **FIPS 205** | **SLH-DSA** (SPHINCS+) |
| Classical Signature | **FIPS 186-5** | **Ed25519** |
| Hybrid Mode | NIST SP 800-227 (Draft) | Hybrid PQC + Classical |

## Why Hybrid Mode?

Hybrid cryptography combines post-quantum algorithms with classical algorithms so that:
1. Security is maintained even if one algorithm is compromised.
2. Protection against both quantum attacks (Shor's algorithm) and classical attacks.
3. Provides a migration path as post-quantum cryptography matures.

## Documentation

Hosted at [QuantumCoin.org](https://QuantumCoin.org).

- [Quantum Resistance Whitepaper](https://quantumcoin.org/whitepapers/Quantum-Coin-Blockchain-Quantum-Resistance-Whitepaper.pdf)
- [Quantum Resistance Overview](https://quantumcoin.org/quantum-resistance.html)
- [FAQ](https://quantumcoin.org/faq.html)

## NIST Post-Quantum Cryptography Standards

The algorithms used by Quantum Coin are standardized by the National Institute of Standards and Technology (NIST):
- FIPS 203: ML-KEM (Module-Lattice-Based Key-Encapsulation Mechanism)
- FIPS 204: ML-DSA (Module-Lattice-Based Digital Signature Algorithm)
- FIPS 205: SLH-DSA (Stateless Hash-Based Digital Signature Algorithm)

These standards were finalized as part of NIST's Post-Quantum Cryptography Standardization project.

## Contributing

Thank you for considering to help out with the source code! 

* Please reach out in [our Discord Server](https://discord.gg/bbbMPyzJTM) for any questions. 
* Pull requests need to be based on and opened against the `main` branch.

## License

This documentation content is provided under the MIT license. Website media, assets and those that are specific to the website theme are not covered under this license.

Since the documentation website currently uses a commercial theme, the assets such as media, css have not been checked into Github. These assets are served separately via a CDN. This documentation will be moved to a better open-source friendly theme in the future.
Changes to this repository is not immediately reflected in the documentation website. It is a manual process currently and will be automated in the future.
