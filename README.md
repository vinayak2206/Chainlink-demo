# Chainlink (LINK): Live Data Feed Demo

Interactive demo for **FLCS #2, DeFi/DAO Case Study**
Principle of Blockchain Technology, Fall 2026
Instructor: Prof. Tumennast Erdenebold

**Live demo:** https://chainlink-defi-demo.vercel.app

## What this project is

Chainlink is a decentralized oracle network. It is **not** a blockchain and **not** a DAO. It is infrastructure that brings real-world data, such as asset prices, to smart contracts.

Blockchains cannot read information outside their own network. DeFi apps like Aave need prices to decide how much a user can borrow and when a loan must be liquidated. This demo shows how Chainlink delivers that price and why an accurate price matters.

## What the demo shows

1. **How a price gets onchain.** Five exchanges report prices, seven independent Chainlink nodes read them, the DON takes the **median**, and a report is written onchain only when the price moves 0.5% or the heartbeat ends. A smart contract then reads the result.
2. **Why it matters (Aave-style loan).** A user deposits 10 ETH and borrows USDC. The health factor is `(10 x price x 0.825) / borrowed`. Below 1, the loan is liquidated.
3. **Two failure tests.** A manipulated exchange price and a faulty node, to show how the median protects the result.

## Controls

| Control | What it does |
|---|---|
| Pause feed / Resume feed | Stops or restarts the automatic price updates (every 1.5 s) |
| Tick once | Runs a single update so you can step through the process |
| ETH market price | Sets the simulated market price |
| Attack: one exchange reports a price 40% too low | A naive single-source oracle wrongly liquidates the borrower, while Chainlink's median ignores the bad source |
| Make one Chainlink node faulty | One of seven nodes reports a price 50% too high, and the median still holds |
| Borrowed USDC | Sets the loan size, which changes the health factor |

## Simulation notice

All prices on the page (exchanges, nodes, DON, onchain report, loan) are **generated in the browser** to explain the mechanism. They are not read from a blockchain.

- The 0.5% update threshold and the 82.5% liquidation threshold are illustrative. Real values differ by feed and by Aave market.
- In the real network, nodes reach agreement off-chain and submit one report. The demo simplifies this step.
- For real data, see the live ETH/USD feed at https://data.chain.link.

## Run locally

No build step or dependencies are needed.

```bash
git clone https://github.com/YOUR-USERNAME/chainlink-defi-demo.git
cd chainlink-defi-demo
```

Then open `index.html` in a browser.

## Deploy

The project is a single static page. On Vercel, import the GitHub repo, set the framework preset to **Other**, leave the build command empty, and deploy.

## Files

```
index.html     The whole demo (HTML, CSS and JavaScript)
favicon.png    Browser tab icon
README.md      This file
```

## Team

| Student ID | Name |
|---|---|
| 202608434 | Yashwanth Gavini |
| 202608430 | Vinayak Bhutra |
| 202608432 | Sushanth Kunde |
| 202608461 | Vu Dung |
| 202019041 | Sahil Khatkar |

All members contributed equally (20% each) to research and presentation.

## Sources

- Chainlink, FAQ and platform overview
- Ellis, Juels and Nazarov, *ChainLink: A Decentralized Oracle Network* (2017)
- Chainlink Documentation: Data Feeds overview and CCIP
- Chainlink, DeFi use cases and Aave integration

<!-- Add final URLs and access dates before submission. -->

## Disclaimer

This is an educational project. It is not financial advice, and the simulated values do not represent real market data.
