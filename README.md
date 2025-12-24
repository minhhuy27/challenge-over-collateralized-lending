# Over-Collateralized Lending Challenge (SpeedRunEthereum)

This project is a decentralized money market protocol built on Ethereum using **Scaffold-ETH 2**. It allows users to deposit ETH as collateral and borrow the stable asset **CORN** (pegged to $1) against it. The system ensures solvency through an over-collateralization mechanism and incentivized liquidations.

This project was developed as part of the **SpeedRunEthereum** challenges.

## 🌟 Features

### Core Functionality (`Lending.sol`)

* **Deposit Collateral:** Users can deposit ETH to back their loans.
* **Borrow Assets:** Users can borrow CORN tokens up to a specific Loan-to-Value (LTV) ratio (maintaining >120% collateralization).
* **Repay Loan:** Users can repay borrowed CORN to unlock their collateral.
* **Liquidation:** If a user's health factor drops below the threshold (due to ETH price drops), liquidators can repay the debt in exchange for the collateral + a liquidation bonus (10%).

### 🚀 Advanced Features (Side Quests)

* **Flash Loan Liquidation (`FlashLoanLiquidator.sol`):** A smart contract that utilizes Flash Loans to liquidate unsafe positions without requiring upfront capital.
* **Leverage Loop (`Leverage.sol`):** A mechanism to loop `Borrow -> Swap -> Deposit` multiple times in a single transaction to maximize ETH exposure (Long ETH).

## 🛠 Prerequisites

Before running the project, ensure you have the following installed:

* [Node.js](https://nodejs.org/en/download/) (v18 LTS recommended)
* [Yarn](https://classic.yarnpkg.com/en/docs/install) (v1 or v2+)
* [Git](https://www.google.com/search?q=https://git-scm.com/downloads)

## 🚀 Quick Start (How to Run)

Follow these steps to set up the environment and run the DApp locally.

### 1. Install Dependencies

Clone the repository and install the necessary packages:

```bash
git clone https://github.com/minhhuy27/challenge-over-collateralized-lending.git
cd challenge-over-collateralized-lending
yarn install

```

### 2. Start the Local Blockchain

Open a **first terminal** window and run:

```bash
yarn chain

```

*This starts a local Ethereum network (Hardhat Network) at `localhost:8545`.*

### 3. Deploy Contracts

Open a **second terminal** window and run:

```bash
yarn deploy

```

*This compiles and deploys your smart contracts (`Lending.sol`, `Corn.sol`, `CornDEX.sol`, etc.) to the local network.*

### 4. Start the Frontend

Open a **third terminal** window and run:

```bash
yarn start

```

*This starts the NextJS application at `http://localhost:3000`.*

---

## 🧪 Testing & Simulation

### Manual Testing

1. Go to `http://localhost:3000`.
2. Use the **Faucet** button (top right) to grab some test ETH.
3. **Approve** the Lending contract to spend your CORN (if repaying).
4. Try depositing ETH, borrowing CORN, and moving the price (using the Debug UI) to trigger liquidations.

### Automated Simulation

To see the system in action with bot accounts interacting with your contracts:

```bash
yarn simulate

```

*This script will create random users who deposit, borrow, and liquidate each other automatically.*

## 📂 Project Structure

* `packages/hardhat/contracts`
* `Lending.sol`: The main logic for the lending protocol.
* `Corn.sol`: The ERC20 token used as the borrowed asset.
* `CornDEX.sol`: A simple AMM used as a price oracle and swapping mechanism.
* `FlashLoanLiquidator.sol`: Logic for flash loan liquidations.
* `Leverage.sol`: Logic for creating leveraged positions.


* `packages/nextjs`: The frontend user interface built with Next.js and RainbowKit.

## 📡 Deployment to Testnet (Sepolia)

To deploy this project to a public testnet like Sepolia:

1. Rename `.env.example` to `.env` in `packages/hardhat`.
2. Add your **Alchemy API Key** and **Deployer Private Key** in the `.env` file.
3. Run the deployment command:
```bash
yarn deploy --network sepolia

```


4. Verify the contract:
```bash
yarn verify --network sepolia

```



## Live Demo

* **Live App (Vercel):** https://over-collateralized-lending-26w9s86iv-huys-projects-d7f14f3b.vercel.app
* **Contract Address (Sepolia):** Lending: https://sepolia.etherscan.io/address/0xa1522313914c7F9431437EE87b91f22C8A653e4e