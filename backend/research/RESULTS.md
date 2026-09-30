# Smart Contract Test Evidence

## Captured Run

- Run date: 2026-09-30
- Result: 8 passing tests, 0 failing tests
- Node.js: 22.20.0
- Hardhat: 2.27.1
- Solidity: 0.8.19, optimizer enabled with 200 runs
- Network: local Hardhat Network, chain ID 1337, 30,000,000 block gas limit

Reproduce from `backend/`:

```sh
npm install
npm test
```

The test suite exercises deployer ownership, owner-only role registration, required role registration, producer-only product creation, the complete valid supply-chain flow, rejection of a producer attempting supplier actions, and rejection of out-of-order stage transitions. The negative transition cases also assert that the product remains in `Product Created` after rejection.

## Gas Results

Hardhat's gas reporter output from the captured run is summarized below. Method values are reporter averages over successful transactions in the test suite; call counts are included because some methods have small sample sizes.

| Operation | Average gas | Successful calls |
| --- | ---: | ---: |
| Contract deployment | 1,701,274 | 8 fixture deployments |
| `addSupplier` | 164,367 | 5 |
| `addProducer` | 164,349 | 5 |
| `addDistributor` | 164,400 | 5 |
| `addSeller` | 164,507 | 5 |
| `addProduct` | 139,493 | 5 |
| `supplyProduct` | 76,363 | 1 |
| `processProduct` | 59,265 | 1 |
| `distributeProduct` | 59,189 | 1 |
| `listForSale` | 56,258 | 1 |
| `markProductSold` | 39,254 | 1 |

The reporter excludes intrinsic transaction gas overhead from its method execution figures. Reverted calls are not represented in this successful-transaction table.

## Interpretation

These results show that the listed authorization and stage-ordering examples behave as asserted under the local test network. They do not establish a general tampering-detection rate: the contract rejects specific invalid calls, and this suite does not test an off-chain detection or alerting system. The gas figures are not latency or throughput measurements, and the small call counts are not a statistical benchmark. Any paper claim should identify this as a local functional test and gas snapshot, not production-chain performance data.