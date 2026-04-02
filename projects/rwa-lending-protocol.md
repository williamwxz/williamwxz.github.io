# Web3 Full Stack - RWA Lending Protocol

**Timeline:** May 2024 - Jan 2025
**Stack:** Solidity, Go, Next.js, wagmi, WebSocket, AWS EKS, PostgreSQL

## Overview

Designed and built a decentralized lending protocol for real-world assets (RWA), enabling businesses to tokenize account receivables as collateral for on-chain loans. Deployed across four EVM-compatible chains.

## Architecture

```
        Lenders / Borrowers
              │
         Next.js + wagmi
         (Vercel frontend)
              │
    ┌─────────┴─────────┐
Solidity Contracts      Go API (EKS)
(4 chains)              (sub-250ms)
    │                      │
    └──── WebSocket ───────┘
          listeners
              │
          PostgreSQL
        (real-time state)
```

## Key Technical Decisions

- **Multi-chain deployment:** Deployed identical Solidity contracts across Ethereum, Arbitrum, Base, and Binance Chain to maximize liquidity pool access. Used a factory pattern for standardized pool creation.
- **Go backend with WebSocket:** Chose Go over Node.js for the backend to handle concurrent WebSocket connections listening to contract events across all four chains. Achieved sub-second event propagation to the database.
- **API performance:** Optimized the Go API layer with connection pooling, query batching, and response caching on AWS EKS. Achieved sub-250ms query latency — a 3x improvement over the initial implementation.
- **wagmi for wallet UX:** Used wagmi + viem on the frontend for type-safe contract interactions, supporting MetaMask, WalletConnect, and Coinbase Wallet.

## Results

- ~$300K total TVL across all pools
- $50K raised per lending pool
- Sub-250ms API latency (3x improvement)
- Sub-second on-chain event propagation
- Team of 5 engineers, concept to production in 6 months
