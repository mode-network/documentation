---
description: >-
  This is an example on how to run a basic agent that performs a task on Mode
  with GOAT
---

# Quickstart

## How to Run Mode Plugin from GOAT

### Prerequisites

* [Node.js v20.12.2](https://nodejs.org/) or higher.
* [Turbo](https://turbo.build/).
* [PNPM](https://pnpm.io/).

### Steps

1. Clone the GOAT repository:

```bash
git clone https://github.com/goat-sdk/goat.git
```

2. Open the repository in your preferred code editor (we'll use VSCode in this example).
3. Install dependencies and build the project:

* Since we are going to test the Mode plugin, which is in the TypeScript folder, we first need to navigate to that directory:

```bash
cd goat/typescript
```

* Then, run the following commands:

```bash
pnpm install
pnpm build
```

4. Set up the Mode plugin:

* Go to the plugin directory:

```bash
cd examples/vercel-ai/mode
```

* Copy the environment configuration file:

```bash
cp .env.template .env
```

* Fill in the .env file with the following values:
  * OPENAI\_API\_KEY: Obtained from [OpenAI](https://platform.openai.com/settings/organization/api-keys).
  * WALLET\_PRIVATE\_KEY: Your wallet's private key. It's important to ensure that the key starts with 0x to avoid execution errors.

5. Rebuild the project:

* Navigate back to the goat/typescript directory and run:

```bash
pnpm install
pnpm build
```

6. Run the Mode plugin:

* Navigate back to the plugin directory:

```bash
cd examples/vercel-ai/mode
```

* Run the following command to start the plugin:

```bash
npx ts-node index.ts
```

* You will see the message:

```bash
Enter your prompt (or "exit" to quit):
```

Ready! You can now interact with the Mode plugin in GOAT.
