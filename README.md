# Supply Chain Blockchain DApp

A blockchain-based supply chain management system designed to improve transparency, traceability, and trust across the movement of goods from raw material supplier to final consumer. The current project implements a decentralized application (dApp) that records product lifecycle events on-chain, links them to specific stakeholder roles, and exposes a web interface for operational management and traceability.

## 1. Project Concept and Motivation

Traditional supply chains are often fragmented, manual, and difficult to audit. They depend on centralized records, paper-based documentation, and multiple disconnected systems, which create problems such as:

- lack of product traceability
- delayed verification of ownership and origin
- risk of counterfeit goods
- limited transparency across suppliers, producers, distributors, and sellers
- poor accountability when products are lost, delayed, or tampered with

This project addresses those challenges by combining blockchain technology with a role-based supply chain workflow. In the implemented design, every participant and every product state transition is represented on-chain, which reduces the possibility of silent data manipulation and creates a shared, tamper-resistant record of product history.

The core research idea is simple but powerful: by storing supply-chain events in a decentralized ledger and restricting state transitions to authorized actor roles, the system creates a trustworthy and auditable lifecycle for products.

## 2. Problem Statement

The current supply chain ecosystem suffers from several operational and trust issues:

- data is maintained in isolated systems owned by different organizations
- it is difficult to validate the provenance of raw materials or finished products
- intermediate states can be altered without traceable authorization
- product movement cannot always be verified by end consumers or regulators
- lack of secure interoperability slows decision-making and compliance

This project proposes a blockchain-backed infrastructure for supply chain visibility where each event is time-stamped, identity-aware, and immutable.

## 3. Research and Functional Objectives

The application is designed to achieve the following goals:

1. Record and validate participant roles within the supply chain.
2. Track product lifecycle stages from creation to sale.
3. Enforce role-based authorization for each business action.
4. Provide a transparent, auditable chain of custody.
5. Enable a user-friendly interface for stakeholders to interact with the blockchain.
6. Demonstrate a practical implementation of blockchain in real-world logistics and product-tracking use cases.

## 4. Current System Design

The current version of the project follows a decentralized architecture with three major layers:

- blockchain layer: Solidity smart contracts running on an Ethereum-compatible network
- application layer: Next.js frontend for interaction and monitoring
- infrastructure layer: Hardhat for contract compilation, deployment, and local development; Ganache for local blockchain simulation; MetaMask for wallet access

### High-Level Architecture

```text
User Interface (Next.js)
        |
        v
Wallet / Browser (MetaMask)
        |
        v
Web3.js / Contract Interaction
        |
        v
Ethereum-Compatible Network
        |
        v
Smart Contract (SupplyChain.sol)
```

The architecture prioritizes clarity and practicality: the frontend does not store product records locally; instead, it retrieves and updates blockchain state through smart contract methods.

## 5. Business Workflow and Product Lifecycle

The system models a product lifecycle across a consortium-style supply chain. The current implementation defines four key actor roles:

- Supplier
- Producer
- Distributor
- Seller

The contract owner is responsible for registering actors and enabling the operational flow. A product moves through the following states:

```text
Created -> Processing -> InTransit -> ForSale -> Sold
```

### Lifecycle Description

1. Product Created
   - A producer creates a product record with a unique identifier, name, and description.

2. Processing
   - The supplier confirms material supply and advances the item to the processing phase.

3. In Transit
   - The producer moves the product into the distribution stage after processing is completed.

4. For Sale
   - The distributor or seller prepares the product for market listing.

5. Sold
   - The seller marks the product as sold, completing the product lifecycle.

These stages are enforced by smart contract logic through `require` statements and state checks, preventing invalid transitions and preserving logical integrity.

## 6. Smart Contract Model

The core logic resides in `backend/contracts/SupplyChain.sol`.

### Main Components

- `ROLE` enum: defines actor types
- `STAGE` enum: defines product lifecycle states
- `Actor` struct: stores identity, role, location, and wallet address
- `Product` struct: stores product metadata and current stage
- mappings for suppliers, producers, distributors, and sellers
- events for actor registration and stage updates

### Core Contract Logic

The contract enforces the following behaviors:

- only the contract owner can register actors
- every actor must have a valid wallet address
- only registered role-holders can perform role-specific actions
- a product cannot advance to an invalid stage without satisfying preconditions
- product movement is permanently recorded as blockchain transactions

Examples of implemented functions include:

- `addSupplier(...)`
- `addProducer(...)`
- `addDistributor(...)`
- `addSeller(...)`
- `addProduct(...)`
- `supplyProduct(...)`
- `processProduct(...)`
- `distributeProduct(...)`
- `listForSale(...)`
- `markProductSold(...)`
- `showStage(...)`

This contract structure is appropriate for research and demonstration purposes because it highlights how blockchain can enforce operational logic without depending on a trusting central authority.

## 7. Frontend and User Experience

The frontend is implemented in the `client` directory using Next.js and TypeScript. It gives users access to a practical dashboard and structured pages for the main operations of the system:

- `register-roles`: adds supplier, producer, distributor, and seller roles
- `order-materials`: creates product records on-chain
- `supply-materials`: advances product stages through workflow actions
- `track-materials`: checks the current progress and transition history of a product

The UI is designed to be simple, dashboard-driven, and operational. It uses a modern component system and a responsive layout so users can interact with the blockchain from a browser without needing to manually handle raw contract calls.

## 8. Technology Stack

### Frontend Stack

- Next.js 14
  - provides app routing, server/client components, and scalable frontend structure
- TypeScript
  - improves maintainability and reduces logic errors in UI and data handling
- Tailwind CSS
  - supports modern, responsive interface design
- Web3.js
  - enables interaction with deployed smart contracts via blockchain RPC and wallet integration
- React-based dashboard components
  - support operational monitoring and workflow management

### Blockchain Stack

- Solidity 0.8.19
  - used for writing the supply chain smart contract logic
- Hardhat
  - provides compilation, testing, and deployment tooling for Solidity contracts
- Ganache
  - offers a local Ethereum network for development and testing
- MetaMask
  - connects the frontend to blockchain transactions and wallet accounts

### Supporting Tools

- Node.js 18+
- npm
- Git and GitHub
- VS Code

### Why this stack is suitable

This combination is widely used in blockchain application research and prototyping because it balances:

- developer productivity
- strong contract testing support
- clear frontend integration with Web3
- realistic local blockchain simulation before deployment

## 9. Project Structure

```text
Supply-Chain-Blockchain/
├── backend/
│   ├── contracts/
│   │   └── SupplyChain.sol
│   ├── scripts/
│   ├── test/
│   ├── ignition/
│   ├── hardhat.config.ts
│   └── package.json
├── client/
│   ├── src/
│   ├── app/
│   ├── public/
│   └── package.json
├── assets/
├── README.md
├── LICENSE
└── ...
```

This structure separates blockchain logic from the user-facing application, making the project easier to explain, maintain, and extend for academic or industrial research.

## 10. End-to-End Workflow of the Current Version

The current implementation operates as follows:

1. The contract owner deploys the smart contract.
2. The owner registers actors with specific supply-chain roles.
3. A registered producer creates a product instance on the blockchain.
4. A registered supplier advances the product from Created to Processing.
5. The producer moves the product to InTransit.
6. A distributor updates the state to ForSale.
7. A seller lists the product and marks it as Sold.
8. The frontend reads the blockchain state and renders the up-to-date lifecycle and records.

This flow demonstrates a digital version of product provenance and custody tracking, where trust is based on blockchain immutability rather than a centralized database.

## 11. Research Significance

This project is relevant to research in the areas of:

- blockchain-based traceability systems
- role-based access control in supply chains
- decentralized application design for business processes
- trust and immutability in logistics and product provenance
- smart contract-driven workflow enforcement

In academic terms, the project is a proof-of-concept for how blockchain can improve transparency, reduce uncertainty, and create traceable records across multi-party supply chain interactions.

## 12. Setup and Execution

### Prerequisites

- Node.js 18+
- npm
- MetaMask
- Ganache
- Git

### Install dependencies

```bash
cd backend
npm install

cd ../client
npm install
```

### Start local blockchain

Use Ganache with the following network settings:

- RPC URL: `http://127.0.0.1:7545`
- Chain ID: `1337`

### Deploy the contract

```bash
cd backend
npx hardhat run scripts/deploy.ts --network ganache
```

### Run the frontend

```bash
cd client
npm run dev
```

Open the application in the browser on:

```text
http://localhost:3000
```

## 13. Current Strengths

- transparent product lifecycle tracking
- role-based permission enforcement
- immutable transaction records
- simple user interface for non-technical users
- clear separation between blockchain logic and app presentation
- useful educational and research demonstration of decentralized supply chain systems

## 14. Limitations and Future Work

The current version is intentionally lightweight and demonstrates the core concept clearly, but it has opportunities for extension:

- integration with IoT-based product verification
- real-time shipment tracking with sensor data
- IPFS storage for large off-chain records
- tokenized asset or NFT-based product ownership models
- advanced compliance and audit features
- integration with external ERP or database systems

These improvements would make the system more suitable for production-grade business environments and broader research validation.

## 15. Conclusion

This project represents a complete end-to-end blockchain supply chain prototype. It begins with a real-world problem in traditional logistics and product tracking, moves through a formal role-based system model, and implements the solution using smart contracts, decentralized infrastructure, and a responsive web application.

The current version demonstrates the practical value of blockchain in supply-chain transparency and traceability. It is especially suitable for academic discussion, prototype demonstrations, and research-oriented exploration of how decentralized systems can improve trust and accountability across multi-actor business networks.

## License

This project is licensed under the MIT License.
- Write clear commit messages
- Add tests for new features
- Update documentation as needed
- Read the full [CONTRIBUTING.md](./CONTRIBUTING.md) before opening a pull request
- Follow the project [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)
- Look for issues labeled `good first issue` or `help wanted` if you’re new to the project

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Documentation

### External Resources

- [Solidity Documentation](https://docs.soliditylang.org/en/v0.8.19/)
- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [Hardhat Documentation](https://hardhat.org/docs)
- [Web3.js Documentation](https://web3js.readthedocs.io/)
- [Ganache Documentation](https://trufflesuite.com/docs/ganache/overview)
- [MetaMask Documentation](https://docs.metamask.io/)



## Show Your Support

If you find this project helpful, please consider:

- Starring the repository
- Forking the project
- Reporting bugs
- Suggesting new features
- Sharing the repository with others

---

<div align="center">

**Made with Solidity, Next.js, and Web3**

[Back to Top](#supply-chain-blockchain-dapp)

</div>
