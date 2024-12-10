# 🏗️ Building your first agent

## Approaches to Building Agents

There are several options to implement an AI agent. LangChain, for example, is a widely-adopted framework, providing Python and JavaScript SDKs equipped with tools for chains, memory systems, and vector stores. The Open Liberated Autonomous Society (OLAS) framework offers specialized components for constructing autonomous economic agents. For developers seeking more granular control, integrating OpenAI's Assistants API or Anthropic's Claude directly into your codebase is possible.

Designing an agent from the ground up requires a focus on several key components: defining actions the agent can perform, establishing connections to platforms such as Telegram, Discord, and other applications, and integrating large language models (LLMs) for advanced processing capabilities, memory, etc. You could start with a foundational server setup, like node.js, to implement these elements, progressively adding features such as persistent memory and tool integration to enhance the agent's functionality.

## Building Your First AI Agent with Eliza and GOAT

### Introduction to Eliza

Eliza is a powerful framework designed to simplify the creation of AI agents. It provides a robust set of tools for building agents that can understand, plan, and execute tasks autonomously. For more information, you can explore the [Eliza GitHub repository](https://github.com/ai16z/eliza) and the [official documentation](https://ai16z.github.io/eliza/docs/intro/).

### Understanding GOAT

GOAT, or the Great Onchain Agent Toolkit, is an open-source framework that equips AI agents with blockchain capabilities, such as managing wallets, trading tokens, and interacting with smart contracts. Within Eliza, GOAT functions as a plugin, significantly enhancing the framework by enabling agents to perform a wide range of on-chain actions seamlessly. This integration allows Eliza agents to autonomously execute blockchain operations. With GOAT, Eliza agents can now manage wallets, trade tokens, and interact with smart contracts, and protocols.

### Upcoming Tutorial

A detailed step-by-step tutorial on building your first AI agent with Eliza and GOAT is in the works. This guide will cover everything from setting up your environment to creating custom plugins and actions.

### Additional Resources

In the meantime, we recommend watching episodes of the AI Dev School, where Shaw demonstrates how to create new plugins and actions.

Part 1: [General Eliza concepts](https://www.youtube.com/watch?v=ArptLpQiKfI)

Part 2: [Plugins & More](https://www.youtube.com/watch?v=XenGeAcPAQo)

Part 3: [Evaluators](https://www.youtube.com/watch?v=Y1DiqSVy4aU)

Stay tuned for more updates and resources to help you get started with AI agent development.
