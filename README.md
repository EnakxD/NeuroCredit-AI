# NeuroCredit — Alternative Credit Scoring on Blockchain

> **Frostbyte Hackathon 2026 Submission**
> Themes: AI/ML · FinTech · Blockchain/Web3 · Financial Inclusion

---

## The Problem

**1.4 billion people** globally are "credit invisible" — no credit history, no CIBIL score, no access to formal loans. This includes India's 400M+ gig workers, freelancers, and informal economy participants who are financially responsible but systematically excluded.

## The Solution

NeuroCredit is a **decentralized alternative credit scoring system** that:
1. Uses **ML (XGBoost)** to score anyone from 300–900 using 14 alternative financial signals (UPI patterns, bill payments, income stability, savings behaviour)
2. Mints the score as a **Soul Bound Token (ERC-5484 SBT)** on Polygon — owned by the user, immutable, non-transferable
3. Allows **lenders to verify** creditworthiness via a public smart contract function — zero personal data exposed

---

## Architecture

```
User Inputs (14 signals)
        │
        ▼
┌───────────────────┐
│  FastAPI Backend  │  ←── orchestrates everything
└────────┬──────────┘
         │
    ┌────┴──────────────┐
    │                   │
    ▼                   ▼
XGBoost ML Model   Polygon Smart Contract
(score 300–900)    (NeuroCredit.sol ERC-5484)
                         │
                    Soul Bound Token
                    (in user's wallet)
                         │
                    Lender calls verifyCredit()
                    ← score + eligibility only
```

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| ML Model | Python · XGBoost · scikit-learn · joblib |
| Backend | FastAPI · Pydantic · Uvicorn |
| Smart Contract | Solidity 0.8.20 · ERC-5484 · Polygon Amoy |
| Frontend | HTML · CSS · Vanilla JS (no framework, fast load) |
| Storage | IPFS (metadata) · On-chain (score + eligibility) |

---

## Key Features

### ML Model
- Trained on 5,000 synthetic profiles mirroring India's informal economy
- 14 input features across 5 categories
- XGBoost with regularisation — MAE < 20 points, R² > 0.95
- Scoring breakdown by category (Payment History, Transaction Activity, Income Stability, Savings Behaviour, Tenure)

### Smart Contract (`NeuroCredit.sol`)
- ERC-5484 Soul Bound Token — permanently bound to wallet, non-transferable
- One SBT per wallet address
- `mintCredit(wallet, score, eligible, metadataURI)` — issuer only
- `updateScore(wallet, newScore, ...)` — refreshable as financial behaviour improves
- `verifyCredit(wallet)` — public lender endpoint, returns score + grade + eligibility
- Transfer locked: `transferFrom` reverts with custom error

### Privacy Model
- Raw financial data **never** stored on-chain
- Lenders only see: score (300–900), grade, eligibility boolean
- Future: ZK-proof layer so even the score derivation is private

---




