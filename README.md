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

🔹 Layer 1 — AI Credit Scoring
14 alternative financial signals across 5 categories
Model: GradientBoostingRegressor
Output: Score (300–900) + explainability breakdown

📈 Performance

MAE: 13.2
R²: 0.84

🔹 Layer 2 — Blockchain Ownership

Score is minted as an ERC-5484 Soul Bound Token

Key Properties:

❌ Non-transferable
👤 User-owned
🔄 Updatable
🔐 Tamper-proof

🔹 Layer 3 — Verification

Lenders call:
verifyCredit(address wallet)
Returns:

Credit score
Grade
Eligibility
Last update timestamp

✅ No personal data exposed

| Layer      | Technologies                        |
| ---------- | ----------------------------------- |
| ML         | Python, scikit-learn, NumPy, Pandas |
| Backend    | FastAPI, Pydantic                   |
| Blockchain | Solidity, Polygon (Amoy), MetaMask  |
| Frontend   | HTML, CSS, JavaScript               |
| Dev Tools  | Hardhat, Git, VS Code               |


🧪 ML Pipeline
5,000 synthetic user profiles
Realistic distributions (UPI, income, savings patterns)
Feature scaling via StandardScaler

Noise added for realism:

ϵ∼N(0,15)

Weighted scoring model:

Payment History — 35%
Transactions — 25%
Income — 20%
Savings — 10%
Stability — 10%

🔗 Smart Contract Features
mintCredit() → Issue SBT
updateScore() → Refresh score
verifyCredit() → Public verification
Transfer functions → Hard-reverted (non-transferable)

🌐 End-to-End Flow
User submits financial behavior data
ML model generates score
Score is minted as SBT
Lender verifies score via blockchain

⚡ Key Innovations
✅ Alternative data scoring for underserved users
🔗 Credit score as user-owned asset
🔒 Privacy-first verification (no raw data exposed)
🌉 Works for both Web2 lenders & DeFi protocols

🧗 Challenges
Defining fair and unbiased signals
Working with early-stage SBT standard (ERC-5484)
Bridging Web2 APIs with Web3 trust models
Preventing synthetic data overfitting

🏆 Achievements
📊 <2.3% scoring error across full range
🔗 Fully working blockchain integration
🔄 End-to-end pipeline functional
🔐 Strong privacy-preserving design

📚 What We Learned
Alternative data must be carefully curated
SBTs enable self-sovereign identity
Adoption depends on ease, not just innovation
Financial inclusion requires real-world understanding

🎯 Vision

A world where financial trust is earned by behavior — and owned by the individual.

🏁 Built For

🏆 Frostbyte Hackathon 2026




