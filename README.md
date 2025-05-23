# Solana USDC Listener

A minimal TypeScript + Express service that:

1. **Webhook Listener**: Receives Alchemy Address Activity webhooks and verifies on-chain 0.01 USDC transfers via Solana’s RPC.
2. **Query Endpoint**: Provides a GET `/api/tx/:hash` to fetch on-chain USDC transfer amounts for any transaction signature.

---

## Prerequisites

* **Node.js** ≥ v14 and **npm** installed
* A **Solana wallet address** funded with SOL to cover fees
* An **Alchemy** account with a Solana Address Activity webhook created for your wallet

---

## 1. Clone & Install

```bash
git clone https://github.com/lst3455/Solana-usdc-listener.git
cd Solana-usdc-listener
```

Install dependencies:

```bash
npm install express @solana/web3.js dotenv
npm install --save-dev typescript ts-node @types/node @types/express
```

---

## 2. Environment Variables

Create a **`.env`** file:

```dotenv
SOLANA_ADDR=YourSolanaAddressHere
USDC_MINT=EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v
SOLANA_RPC_URL=https://api.mainnet-beta.solana.com
PORT=3000
```

* **SOLANA\_ADDR**: Wallet address need to monitor
* **USDC\_MINT**: Official USDC SPL token mint
* **SOLANA\_RPC\_URL**: Optional; defaults to mainnet-beta RPC

---

## 3. Project Structure

```
solana-usdc-listener/
├── src/
│   └── index.ts        # Main Express app
├── tsconfig.json
├── package.json
└── .env
```

---

## 4. Running the Server

```bash
npx ts-node src/index.ts
```

* Uses **ts-node** to execute TS without compiling first.

---

## 5. Expose Locally via ngrok

1. Run ngrok on port 3000:

   ```bash
   ngrok http 3000
   ```
2. Copy the HTTPS URL and set it as your Alchemy webhook callback:

   ```
   https://<your-ngrok-id>.ngrok.io/api/webhook
   ```

---
