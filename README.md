# ChainLegal: Smart Contract Legal Framework

A comprehensive smart contract system built on Stacks blockchain for managing legal contracts, digital signatures, compliance validation, dispute resolution, and enforcement mechanisms.

## 🚀 Overview

ChainLegal provides a complete legal framework for creating, managing, and enforcing legal agreements on the blockchain. It combines traditional legal concepts with smart contract automation to create a transparent, immutable, and efficient legal system.

### Key Features

- **Legal Contract Management**: Create and manage legal contracts with templates
- **Multi-Jurisdiction Support**: Handle contracts across different legal jurisdictions
- **Digital Signatures**: Secure signature collection with witness and notarization support
- **Compliance Validation**: Automated compliance checking based on jurisdiction-specific rules
- **Dispute Resolution**: Built-in arbitration system for contract disputes
- **Legal Entity Verification**: Registry and verification system for legal entities
- **Enforcement Actions**: Automated enforcement mechanisms for contract violations

## 🏗️ Architecture

### Core Components

1. **Legal Framework Core** (`chainlegal.clar:1-262`)
   - Constants and error handling
   - Legal contract and template structures
   - Jurisdiction registry with initial support for US-NY, UK-ENG, DE-BW
   - Legal entity registration and verification

2. **Digital Signatures & Compliance** (`chainlegal.clar:263-491`)
   - Digital signature collection and validation
   - Compliance rules engine
   - Contract finalization with compliance checks
   - Notarization support

3. **Dispute Resolution & Enforcement** (`chainlegal.clar:492-784`)
   - Dispute filing and management
   - Arbitrator registration and assignment
   - Dispute resolution with binding outcomes
   - Contract enforcement actions

## 📋 Contract Structure

### Legal Contracts
```clarity
{
  template-id: uint,
  creator: principal,
  parties: (list 10 principal),
  jurisdiction: (string-ascii 8),
  contract-type: (string-ascii 32),
  created-at: uint,
  expires-at: uint,
  status: (string-ascii 16),
  terms-hash: (string-ascii 64),
  metadata-uri: (string-ascii 256),
  total-value: uint,
  required-signatures: uint,
  current-signatures: uint
}
```

### Contract Templates
```clarity
{
  name: (string-ascii 64),
  category: (string-ascii 32),
  jurisdiction: (string-ascii 8),
  creator: principal,
  template-hash: (string-ascii 64),
  compliance-level: (string-ascii 16),
  usage-count: uint,
  is-verified: bool,
  created-at: uint
}
```

## 🔧 Usage

### 1. Create a Contract Template

```clarity
(contract-call? .chainlegal create-contract-template
  "Employment Agreement"
  "employment"
  "US-NY"
  "template-hash-123"
  "standard")
```

### 2. Create a Legal Contract

```clarity
(contract-call? .chainlegal create-legal-contract
  u1  ;; template-id
  (list 'SP1ABC... 'SP2DEF...)  ;; parties
  "US-NY"  ;; jurisdiction
  "employment"  ;; contract-type
  u1000000  ;; expires-at (block height)
  "terms-hash-456"  ;; terms-hash
  "ipfs://metadata-uri"  ;; metadata-uri
  u50000  ;; total-value
  u2)  ;; required-signatures
```

### 3. Sign a Contract

```clarity
(contract-call? .chainlegal sign-contract
  u1  ;; contract-id
  "signature-hash-789"  ;; signature-hash
  none)  ;; witness (optional)
```

### 4. File a Dispute

```clarity
(contract-call? .chainlegal file-dispute
  u1  ;; contract-id
  'SP2DEF...  ;; defendant
  "breach-of-contract"  ;; dispute-type
  "evidence-hash-abc")  ;; evidence-hash
```

## 🌍 Supported Jurisdictions

- **US-NY**: New York, United States (UCC-compliant, common law)
- **UK-ENG**: England and Wales (UK contract law, common law)
- **DE-BW**: Baden-Württemberg, Germany (BGB-compliant, civil law)

## 📜 Contract Types & Compliance

### Employment Contracts (US-NY)
- Minimum 2 signatures required
- 24-hour cooling period (~144 blocks)
- No witness or notarization required

### Real Estate Contracts (US-NY)
- Minimum 2 signatures required
- 7-day cooling period (~1008 blocks)
- Witness and notarization required

### Commercial Contracts (UK-ENG)
- Minimum 2 signatures required
- 12-hour cooling period (~72 blocks)
- No witness or notarization required

## 🔐 Security Features

- **Multi-signature validation**: Contracts require signatures from all specified parties
- **Expiration handling**: Contracts automatically expire after specified block height
- **Jurisdiction validation**: Only supported jurisdictions are accepted
- **Entity verification**: Legal entities must be registered and verified
- **Arbitrator certification**: Arbitrators require certification and activation

## 🛠️ Development

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) - Stacks smart contract development toolchain
- Node.js and npm
- Stacks wallet for testing

### Setup

1. Clone the repository
```bash
git clone <repository-url>
cd ChainLegal
```

2. Install dependencies
```bash
cd chainlegal
npm install
```

3. Run tests
```bash
clarinet test
```

4. Deploy to devnet
```bash
clarinet deploy --devnet
```

### Project Structure

```
chainlegal/
├── contracts/
│   └── chainlegal.clar          # Main smart contract
├── tests/
│   └── chainlegal.test.ts       # Contract tests
├── settings/
│   ├── Devnet.toml             # Devnet configuration
│   ├── Testnet.toml            # Testnet configuration
│   └── Mainnet.toml            # Mainnet configuration
├── Clarinet.toml               # Clarinet project configuration
├── package.json                # Node.js dependencies
├── tsconfig.json              # TypeScript configuration
└── vitest.config.js           # Test configuration
```

## 📊 Error Codes

| Code | Error | Description |
|------|-------|-------------|
| 401 | `ERR_UNAUTHORIZED` | Caller lacks required permissions |
| 402 | `ERR_CONTRACT_NOT_FOUND` | Contract or resource not found |
| 403 | `ERR_INVALID_JURISDICTION` | Unsupported jurisdiction |
| 404 | `ERR_CONTRACT_ALREADY_SIGNED` | Party has already signed |
| 405 | `ERR_CONTRACT_EXPIRED` | Contract past expiration |
| 406 | `ERR_INVALID_PARTY` | Caller not a contract party |
| 407 | `ERR_INSUFFICIENT_SIGNATURES` | Not enough signatures collected |

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🔗 Links

- [Stacks Documentation](https://docs.stacks.co/)
- [Clarity Language Reference](https://docs.stacks.co/clarity/)
- [Clarinet Documentation](https://github.com/hirosystems/clarinet)

## 🚨 Disclaimer

This smart contract system is for educational and development purposes. Before using in production:

1. Conduct thorough security audits
2. Verify compliance with local laws and regulations
3. Test extensively on testnets
4. Consider legal implications in your jurisdiction
5. Ensure proper key management and access controls

Legal contracts on blockchain should complement, not replace, traditional legal frameworks and professional legal advice.