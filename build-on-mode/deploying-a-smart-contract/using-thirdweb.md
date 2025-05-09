---
description: >-
  How to deploy a smart contract on Mode with ThirdWeb CLI & Smart contract
  Dashboard
---

# Using Thirdweb

Thirdweb is a complete web3 development framework that provides everything you need to connect your apps and games to decentralized networks. Mode is now integrated with Thirdweb, allowing you to use all these fantastic features to deploy and interact with your smart contracts quickly.

{% hint style="info" %}
This guide assumes you have got Sepolia ETH and bridged to the Mode Testnet Network.&#x20;
{% endhint %}

{% hint style="info" %}
You can use deploy pre-built contracts direct from the [thirdweb dashboard](https://portal.thirdweb.com/contracts/explore/overview?utm_source=modedocs&utm_medium=docs) as another option.&#x20;
{% endhint %}

## 1. Download the ThirdWeb CLI

We’ll go through the steps of installing and running the Thirdweb CLI, but if you encounter any issues with these steps, please refer to the [official documentation](https://portal.thirdweb.com/cli/create).&#x20;

To download the Thirdweb CLI globally, open a terminal and run the following command:\
\
`npm i -g thirdweb`

Now try running:\
\
`thirdweb --version`\
\
if the CLI is installed correctly, you will be prompted to go to the installed version.

## 2. Create the Local Environment

Let’s create a new project to work on our local machine using the command:\
\
`npx thirdweb create`

You will be prompted with a menu with different options to help you set up your environment for coding the smart contract. For the sake of this tutorial, we will be deploying an ERC-20 token and adding the Drop extension from Thirdweb. This will set up a basic ERC-20 token with the possibility to mint, burn, and airdrop tokens from the dashboard. What’s even better is that these contracts are all audited and ready to deploy!

Follow the following screenshot to create an example smart contract, or you can use your own code.

<figure><img src="https://lh3.googleusercontent.com/4oIJmVWET14ccRu4lAcqFMc2GZrBJcXzdJF6UvaH2CAOCY5m7s9SZZaKKViBxOViEW-RcBooGKlFFleX286ip6rwqqN0Sx4IS-9aR64VZRUv0XUVBZRo5BT9vlhrnekNxZMqsXO20ES0lNcYV2ycJ44" alt=""><figcaption></figcaption></figure>

After a few seconds, you should now have a folder called “my-mode-token” or whatever you named your project.&#x20;

To modify your smart contract, you can launch Visual Studio Code (or your preferred code editor) and access the designated project folder. We will leave it as is since we want to focus on showing the deployment process. We already have a fully functional smart contract code thanks to thirdweb’s templates.

## 3. Create a ThirdWeb API Key

Thirdweb services require an API key, so let’s create one. There is an official tutorial [here](https://blog.thirdweb.com/changelog/api-keys-to-access-thirdweb-infra/) but let’s go through it quickly.\
\
To get an API key, go to [https://thirdweb.com/dashboard/settings/api-keys](https://thirdweb.com/dashboard/settings/api-keys).\
\
Connect your wallet and you will be prompted with a message to sign from Metamask (you can use other wallets if you prefer). Once your wallet is connected, you should be able to switch to Mode network and also Create an API Key.

<figure><img src="https://lh3.googleusercontent.com/fGJoHbCOPwfPw7oZChraQaMMK1H4EzcyizWMUlX-MYlpb28FrRj_1wNqlRYnE49rxvzm3hA22Q6L6Yk1YK_123yny8GFpWY-B53FATKRpUQQ8aGPMx_dN281YPchcM8TuWT9ucCf3pYMx8Es839RqOI" alt=""><figcaption></figcaption></figure>

Follow the steps as shown below

\
![](https://lh5.googleusercontent.com/ZIzthFACIeR8Vcb5H1BavHD8l-xHkTi3Eq1YqCXCAWky94SZiJEp7QIHbxL-eQ5eBjgCYeY\_\_SJ7C6LiCgbeH6mDF4UcMrjRNWuc4jNVdPNCuPBZIAH4IVTLeDm\_YMunu5y1b0d3Ua7xFBFLaAtYw5I)![](https://lh3.googleusercontent.com/aguPxJop2uFe2JMY3HVsrGNldl2T0KD-Rp8vJVXQR\_fHzfIU8JE7BJk5q\_ysWuKShW\_cZHp5RKghI0LfU0\_x\_pb9bz2w2kyo1xkOoj9XyQDDUgHH\_QZitmifuGBHeXQ1i93b8YV9yMb4nJIS9-oq-ho)

It’s very important that you now save your Client ID and Secret Key securely. Don’t lose this because if you do, you must create a new API key.

<figure><img src="https://lh5.googleusercontent.com/Hljcafl_tXKmd_1NrRLxXA7VOnNnEbAMoNCBk_FsY5d1YE35bKVx_tq2I13WdxCemNjl4c_dWMPl0mwtJ-1-8O0_Gp2az1fSpn8I4fz9nE2RZrDequaW_7hCTFVqn7q4mH5r-HkrENyfcsIpfZ7gTcU" alt=""><figcaption></figcaption></figure>

## 4. Deploy

Now, when your contract is ready to deploy, run the following command at the root of your project:\
\
`Npx thirdweb deploy`

You should be prompted with something similar to this:

<figure><img src="https://lh6.googleusercontent.com/mEFhvKgccMQ_i1BMY07N1Pbyl70LRs9YpCk3KySt8ByOtJlXaWydo6Jq2tTD6lJkw_sGYhzHxKcwYTwBxdzDy2rlCN0j-7RI0nHlyj43rxRDAplqZBW2p-CLNI6ZB86Z4moys54ATHSYZ-TnELpAERY" alt=""><figcaption></figcaption></figure>

If your browser doesn’t automatically pop up with the link to deploy your contract, just copy the link shown in the terminal and paste it into a browser.

Select the Mode testnet network from the search list

<figure><img src="https://lh5.googleusercontent.com/wvFpjpxBgIeZyPGMETJkIg-3UD8QvZIeR0BJ2C7uvhQ-tZkpXDAcSaFVsQQzmVtcC4ozo0jS_lepDojuMw1UQnbSImeFzaNicAIP2bxQZD8mfikd8TyLv8b78dRGPQ-QoDm-XJDLYyBm1bPAZcb2L4o" alt=""><figcaption></figcaption></figure>

A screen like the one below should appear; just fill in the fields with the names and values you want for your contract parameters. When you are done, just hit Deploy Now. This will cost you gas paid in ETH. This transaction might fail if you don’t have enough ETH on Mode for gas.

Also, make sure to tick the box to add a dashboard for our contract. This will give us some exciting features to interact with our contract later on.

<figure><img src="https://lh3.googleusercontent.com/wECUgA6dG3Vo7hpT0rVoDuftCRpDliQm8P14aec_hYc_wrRg_LGhowFu9XOGrGFgG6aw4yJgHnHwsxbLPOBa284llfLyhCnIsbsNVNZpEz9HHZ3GCSaTxQmN3bFnGR0m0utyHa2M1EZUDJ7RVMv_Dfw" alt=""><figcaption></figcaption></figure>

You will also have to sign a transaction to approve the dashboard, but this step is gasless.&#x20;

That’s it! You have successfully deployed a smart contract to Mode with the Thirdweb CLI!

## 5. Smart Contract Dashboard

To track all your smart contracts and easily interact with them, Thirdweb provides us with a contracts dashboard. Just go to [https://thirdweb.com/dashboard/contracts](https://thirdweb.com/dashboard/contracts) and you will see all your deployed contracts.

<figure><img src="https://lh3.googleusercontent.com/2nbShWLWTkSnIAdskIK-Ph_mco2WYGq6pSoucNN78Nj1GRETFWaFDJ8-AHk5vQomzNHs_uoVeqt6UGZOm5IXSNnIZIiotL7-DFVFhauoeH-d7ZRnpq5KMTRILcNXT2aWaHrOeQzImcesDWunZLrWPbw" alt=""><figcaption></figcaption></figure>

Now just click on the smart contract you want to see the whole dashboard and start playing around!

For example, you can go to the explorer tab and see all the read-and-write methods your contract has and even use them. It’s super easy to just look at variables and manually test out some methods.

<figure><img src="https://lh5.googleusercontent.com/RqDMTSa6OhOvdBPR8ch7YcZJqGwevWUVgNvvqBkEDBa9J6BMxC1lMd3FQ3LcHiwUL-k3-GmdjKidBg6iXVqZzhgprZft9T7mue4-uNLfgxBZ1WbfifuDolLYkaPK3sXYBAmUnHMxRI4BRGi1-SOkfVE" alt=""><figcaption></figcaption></figure>

One of the features we liked the most was the “Build” tab in your smart contract dashboard. This section will have a lot of examples of code snippets to connect with your smart contract programmatically from an app. You can choose between several languages and frameworks, such as Javascript, React, and Python.\
\


<figure><img src="https://lh3.googleusercontent.com/aWeDDj0x77Elg_9l0l0mdkf-U9mt7QCCUgCVHo9OzlL6GYHo5cQxdTgx_ccRWeHyEBGimHbA0cK95bc3FGxH2Oa-fGyBhR2Ya9biR7S6WsKXWrzyK4uVeUlbVECYK8_4xE_fKlpmJbjb8LiT7piqng0" alt=""><figcaption></figcaption></figure>

Congratulations! Now you have created and deployed a smart contract on Mode using the Thirdweb CLI. To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋
