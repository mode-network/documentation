---
description: This guide provides comprehensive documentation on Mode Trade Agents, including setup, management, and best practices.
---

# Mode AI Trading Agents Documentation

## 1. Introduction

### What are Mode AI Trading Agents?

Mode AI Trading Agents are automated trading assistants that help you trade more consistently. They are designed to handle execution, risk management, and trade monitoring so you don’t have to make decisions in the heat of the moment.  
Instead of constantly watching the markets or second-guessing your plan, an agent executes according to the rules you set. It helps you avoid emotional trading, manage entries and exits, and remain consistent over time.

**What they are not:**

- Agents do **not** guarantee profits.
- Agents are **not** substitutes for learning the basics of trading.
- Agents are **not** immune to market risk. **Losses are possible and should be expected.**

### Why use them

- Reduce emotional decisions when trading.
- Maintain consistent execution of your strategy.
- Save time — agents run even when you are offline.
- Learn in a controlled environment with risk limits built in.

## 2. Getting Started

### Step 1: Create a Sub-Account

- Each agent must run in its **own sub-account**.
- Only **one agent is allowed per sub-account**.
- You must fund the sub-account before launching an agent.

> **Example:**  
> If you want to test an agent with $50, create a sub-account named “Test Agent,” transfer $50, and then launch the agent there.

### Step 2: Choose a Strategy

When creating an agent, select a strategy type that fits your preferred style:

- **Breakout Trading:** Takes a trade once price breaks out, and holds while it has momentum.
- **Trend Following:** Designed to ride longer market trends, and closes the trade once it finishes.

Each strategy has its own focus. Choose the one that aligns best with your goals and expectations.

### Step 3: Configure Risk

Every agent requires risk settings:

- **Timeframe:** Select the timeframe on which it should operate (time-based candles).
- **Leverage:** Multiplies your trading power, but also your exposure to risk.
- **Limits:**
  - Maximum position size: **$5,000**
  - Minimum order size: **$10**
  - Your sub-account balance multiplied by your chosen leverage must be at least **$10**

### Step 4: Launch Your Agent

When you click **“Create Agent”**:

- A new API key is generated for your sub-account and stored securely.
- The API key only allows trading actions and cannot withdraw funds.
- Your agent begins running and will place trades automatically when conditions match the strategy settings.

## 3. Monitoring Agents

After launching, your agents can be monitored directly in the dashboard.  
Each agent card shows:

- Strategy name and trading pair
- Sub-account it is running on
- Current status (running, paused, or error)

Expanding an agent card provides more detail:

- Trade log showing recent entries, exits, or signals
- Timeframe and parameters used
- Last update timestamp
- Controls to edit, pause, or stop the agent

## 4. Managing Agents

### Pausing and Stopping

- You can **pause** an agent to temporarily stop new trades.
- **Stopping** an agent fully disables it, and gives you the option to manage open trades yourself, or close them.

### Editing Agents

- You may edit risk or parameters directly from the agent card by clicking **manage agent**.
- Changes take effect immediately.

### Manual Interference

Agents are designed to manage trades automatically.  
If you manually close or resize a position, the agent may become misaligned with its strategy and produce unexpected results.  
For best outcomes, **avoid manual intervention**.

## 5. Best Practices

- Always fund sub-accounts with an amount you are comfortable risking.
- Do not rely on leverage beyond your understanding.
- Start small and scale up gradually once you are confident.
- Use agents as tools to support your thesis and intent, **not as a guarantee of profit**.
- Review performance regularly and learn from results.

## 6. Frequently Asked Questions

**Why is my PnL different from someone else’s?**  
Execution varies due to slippage, liquidity, and timing. Your prices and PnL will not always match other users running the same agent.

**Why can’t I run multiple agents in one sub-account?**  
To prevent strategies from conflicting with each other, only one agent can operate per sub-account.

**What happens if my balance multiplied by leverage is below $10?**  
Orders will not execute, as the minimum order size on Mode Trade is $10.

**Can the API key withdraw my funds?**  
No. The keys created for agents are restricted to trading actions only.

**What if I manually close an agent’s trade?**  
This may cause the agent to behave unexpectedly. It is recommended not to manually interfere with trades once an agent is running.

## 7. Disclaimer and Risk Notice

Trading with Mode Trade Agents involves risk. By creating an agent, you agree to the following:

- Trading digital assets is highly risky. Losses are possible, including the loss of all funds in a sub-account.
- Agents are intended to assist with consistency and execution, not to guarantee profit.
- Your results may differ from others due to slippage, liquidity, and market conditions.
- Each agent must run in a separate sub-account. Sub-accounts must be funded before launching an agent.
- Maximum position size per agent is $5,000. Minimum order size is $10.
- A new API key is created when an agent is launched. This key is stored securely, permits trading only, and cannot withdraw funds.
- Manual closing or modification of trades may interfere with an agent’s performance and is not recommended.

> **You accept full responsibility for the use of agents, including financial outcomes, and acknowledge that Mode Trade is not liable for losses or damages.**

By clicking **“Create Agent”**, you confirm that you have read, understood, and agree to these conditions.

## 8. Appendix: Glossary

- **PnL (Profit and Loss):** The amount you have gained or lost on trades.
- **Leverage:** A multiplier of account size that increases both potential profit and risk.
- **Slippage:** The difference between the expected price of a trade and the actual executed price.
- **Sub-Account:** A separate trading account within your main Mode Trade account, used to isolate each agent.
- **API Key:** A secure digital key allowing trading actions on your account. Keys used by agents cannot withdraw funds.
