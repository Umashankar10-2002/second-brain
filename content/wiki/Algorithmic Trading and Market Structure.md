---
title: "Algorithmic Trading and Market Structure"
type: synthesis
created: 2026-05-09
updated: 2026-05-09
sources:
  - "wiki/Reinforcement Learning Trading Bot in Python  Train an AI Agent on Forex (EURUSD).md"
  - "wiki/The Man Who Crashed The Stock Market From Home.md"
tags:
  - trading
  - algorithmic-trading
  - market-structure
  - reinforcement-learning
---

# Algorithmic Trading and Market Structure

## Thesis

Algorithmic trading should be understood at two levels: the agent or strategy level, and the market-structure level. A trading bot can optimize local behavior, but markets are shared systems where liquidity, order-book signals, incentives, and automation can interact in unstable ways.

## Source Signals

- [[wiki/Reinforcement Learning Trading Bot in Python  Train an AI Agent on Forex (EURUSD)]] presents the agent-level view: observations, actions, rewards, and policy learning on historical forex data.
- [[wiki/The Man Who Crashed The Stock Market From Home]] presents the market-structure view: spoofing, fragile liquidity, high-frequency trading, and the 2010 Flash Crash.

## Useful Distinction

| Layer | Question | Risk |
|---|---|---|
| Agent strategy | What action should the model take next? | Overfitting, unrealistic rewards, weak risk controls. |
| Execution | How does the order enter the market? | Slippage, latency, fill assumptions. |
| Market structure | What does the system do when many agents react? | Fragile liquidity, feedback loops, spoofing, flash events. |

## Practical Use

Treat backtested trading agents as educational artifacts unless they include realistic execution, transaction costs, risk limits, and out-of-sample validation. The market-structure examples show why profitable-looking local behavior can still be dangerous when it interacts with real liquidity.

## Related

- [[wiki/Reinforcement Learning Trading Bot in Python  Train an AI Agent on Forex (EURUSD)]]
- [[wiki/The Man Who Crashed The Stock Market From Home]]

