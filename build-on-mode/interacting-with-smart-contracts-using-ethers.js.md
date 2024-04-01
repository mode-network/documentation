---
description: >-
  How to interact with smart contracts deployed on Mode from a frontend using
  ethers.js
---

# Interacting with Smart Contracts using ethers.js

In this tutorial, we'll walk through setting up a basic web app, deploying a smart contract on MODE Network's testnet, and interacting with it using ethers.js.

{% hint style="info" %}
If you want a quickstart and just get to the code, go to [this repository](https://github.com/joshuanwankwo/mode\_testnet) and follow the readme guide to run it. We will walk you through the code in this tutorial.
{% endhint %}

## Prerequisites

* Add MODE Testnet to your metamask using the network info from here:[network-details.md](../mode-testnet/network-details.md "mention")
* Get test ETH sepolia here: [testnet-faucets.md](../tools/testnet-faucets.md "mention")
* Bridge to MODE testnet here: [bridging-to-mode-testnet.md](../mode-testnet/bridging-to-mode-testnet.md "mention")
* Have [Node and NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) installed on your PC
* Have a basic understanding of React.js and how blockchain works

## Smart Contract Deployment On Mode

We've crafted a simple smart contract named BidBoard for this tutorial. The contract allows advertisers to bid for space on an advertising board. The code and deployment details are available on this [GitHub](https://github.com/joshuanwankwo/mode\_testnet) repository and [Mode Testnet Explorer](https://sepolia.explorer.mode.network/address/0x7215c347458DB86531f3c4Cae1c60c0B93e435Ce). You can also write your own custom smart contract and deploy it to Mode by following [deploying-a-smart-contract](deploying-a-smart-contract/ "mention").

## Getting Started&#x20;

Now that we have the prerequisites, the first thing we need to do is to open our terminal, navigate into the folder where you want your project to be, and create a simple react app by running the following command

`npx create-react-app bidboard-ui`

It should create the whole React App for you.

## Install Ether.js

Ethers.js is a sleek library facilitating the interaction between web applications and blockchain. In the App component, we are using ethers.js to interact with our smart contract and also listen to events being emitted from the smart contract. To install ethers.js, navigate into the project you just created and run the following command:

`npm install ethers`

## Create Main App Component

You can open up the project in VSCode or any other code editor of your choice and then open the <mark style="color:yellow;">`App.js`</mark> file

Replace all the code and paste this:

{% code title="App.js" lineNumbers="true" %}
```jsx
import React, { useState, useEffect } from "react";
import "./App.css";
import { ethers } from "ethers";

const App = () => {
 return (
   <div className="app">
     <h1>hello</h1>
   </div>
 );
};

export default App;
```
{% endcode %}

In this file are importing <mark style="color:orange;">`useState`</mark> and <mark style="color:orange;">`useEffect`</mark> which we'll be needing later in this tutorial, we’re also importing <mark style="color:orange;">`ethers`</mark> to enable us to make a connection to our smart contract.

\
The next thing we need to do is to declare our contract address and ABI file, there are different ways get the contract ABI but if you deployed you smart contract using foundry, you can find your ABI check the following directory:&#x20;

./out/MyContract.sol/MyContract.json.

On the frontend side of things, we’re going to update our <mark style="color:yellow;">`App.js`</mark> adding these lines:

```tsx
 const contractAddress = "0x7215c347458DB86531f3c4Cae1c60c0B93e435Ce";
 const abi = [ ABI JSON CODE ] 

 const [currentAd, setCurrentAd] = useState("Hello World!");
 const [currentBid, setCurrentBid] = useState(0);
 const [advertiser, setAdvertiser] = useState("0x0");
 const [newAd, setNewAd] = useState("");
 const [bidAmount, setBidAmount] = useState("");
 const [provider, setProvider] = useState(null);
 const [status, setStatus] = useState("");
```

Your <mark style="color:yellow;">`App.js`</mark> should look like:

<pre class="language-jsx" data-title="App.js" data-line-numbers><code class="lang-jsx">import React, { useState, useEffect } from "react";
import "./App.css";
import { ethers } from "ethers";

const contractAddress = "0x7215c347458DB86531f3c4Cae1c60c0B93e435Ce";
const abi = [ <a data-footnote-ref href="#user-content-fn-1">YOUR ABI JSON CODE HERE</a> ] 

const App = () => {
 const [currentAd, setCurrentAd] = useState("Hello World!");
 const [currentBid, setCurrentBid] = useState(0);
 const [advertiser, setAdvertiser] = useState("0x0");
 const [newAd, setNewAd] = useState("");
 const [bidAmount, setBidAmount] = useState("");
 const [provider, setProvider] = useState(null);
 const [status, setStatus] = useState("");

 return (
   &#x3C;div className="app">
     &#x3C;h1>hello&#x3C;/h1>
   &#x3C;/div>
 );
};

export default App;
</code></pre>

We added the contract address, the abi, and a few states that we will need for our dApp to work. Don't worry about all these React states, they are particular for this app so you don't need to fully understand them. Please remember to paste you ABI in your App.js file.

{% hint style="info" %}
Usually we would save the ABI in a different file and then import it but in this case we'll just paste all the ABI JSON in our App.js file.
{% endhint %}

## Set the Provider

As the page loads, we'll set our provider to immediately fetch the current advertisement details from our smart contract, as demonstrated in the code below.

```tsx
useEffect(() => {
   if (typeof window !== "undefined") {
     if (window.ethereum) {
       setProvider(new ethers.BrowserProvider(window.ethereum));
       // getCurrentAd()
     } else {
       console.error("Please install MetaMask!");
     }
   }
 }, []);
```

This code is using the `useEffect` hook in React to execute once after the component mounts. If the `window` object and `window.ethereum` are defined, it sets a new provider using `ethers.BrowserProvider` to interact with the Ethereum blockchain. If `window.ethereum` is not defined, it logs an error asking to install MetaMask, a browser extension for managing blockchain transactions.

## Fetch Current Advertisement Data

Create a function to fetch the current advertisement data from our contract and call this function inside a `useEffect` hook.

```tsx
async function fetchCurrentAd() {
   try {
       // Get the provider, instantiate the contract and then call getCurrentAd
       const provider = new ethers.BrowserProvider(window.ethereum);
       const contract = new ethers.Contract(contractAddress, abi, provider);
       const adData = await contract.getCurrentAd();
       
       setCurrentAd(adData[0]);
       setAdvertiser(adData[1]);
       setCurrentBid(ethers.formatEther(adData[2]));
       console.log(adData[0]);
   } catch (error) {
     console.error('Error fetching current ad:', error);
   }
 }

 useEffect(() => {
   fetchCurrentAd();
 }, []);
```

In the above code we’re fetching the current ad by setting our provider like we did before, creating a new instance of our contract by passing in the contract address, contractABI and our provider and then invoking the `getCurrentAd` function from our smart contract which returns the current adData. Then we pass the adData into our app state so we can render them in the frontend.

## Update Our Smart Contract State

Now we’re able to fetch the current state of our contract we also need to be able to update the state and that’s what the below function does

```tsx
 const submitBid = async () => {
   
   const contract = new ethers.Contract(contractAddress, abi, provider); // Instantiate the contract
   const signer = provider.getSigner(); // Assumes Metamask or similar is injected in the browser
   const contractWithSigner = contract.connect(await signer);
   
   try {
     const tx = await contractWithSigner.updateMessage(newAd, {
       value: ethers.parseEther(bidAmount),
     });
     setStatus("Transaction sent, waiting for confirmation...");
     await tx.wait();
     setStatus("Transaction confirmed!");
   } catch (err) {
     console.error(err);
     setStatus("Error: " + err.message);
   }
 };
```

In summary, the <mark style="color:blue;">`submitBid`</mark> function allows users to submit a new bid to the smart contract. It initializes a contract instance and a signer, creates a transaction to update the advertisement message with the new bid, and waits for the transaction to be confirmed on the blockchain.&#x20;

If any errors occur during this process, they are caught and logged, and the user is informed about the error through a status message.

<details>

<summary>Detailed explanation of the submitBid function</summary>

**Contract and Signer Initialization**

* A new contract instance is created using the ethers.Contract constructor with the provided contract address, ABI, and provider.
* A signer, which is essential for authorizing transactions, is obtained from the provider.
* The contract instance is then connected with the signer to authorize interactions.

**Transaction Creation and Sending:**

* A new contract instance is created using the ethers.Contract constructor with the provided contract address, ABI, and provider.
* A signer, which is essential for authorizing transactions, is obtained from the provider.
* The contract instance is then connected with the signer to authorize interactions.

**Transaction Confirmation:**

* The await tx.wait(); line waits for the transaction to be confirmed on the blockchain.
* Once confirmed, a status message is updated to inform the user of the successful transaction.

**Error Handling:**

* If an error occurs at any point in the process, it's caught, logged to the console, and a status message is set to inform the user about the error.

The function leverages async/await syntax to handle the asynchronous operations of sending and waiting for the transaction confirmation in a readable manner.

</details>

## Listening to events on our Smart Contract

Consider you're bidding for ad space, and someone else places a higher bid. It's essential to know about this new bid immediately. This is where event listening helps: it can notify you about the latest bid in real-time, keeping you updated on the bidding activity.

The following code sets up an event listener:

```tsx
useEffect(() => {
   const setupEventListener = async () => {
     if (typeof window.ethereum !== "undefined") {
       const provider = new ethers.BrowserProvider(window.ethereum);
       const contract = new ethers.Contract(contractAddress, abi, provider);
       contract.on(
         "MessageUpdated",
         (newMessage, newAdvertiser, newAmount, event) => {
           // Update your state variables here
           setCurrentAd(newMessage);
           setCurrentBid(ethers.formatEther(newAmount));
           setAdvertiser(newAdvertiser);
         }
       );
       // contract.getEvent
       console.log("Provider:", provider); // Debug line
     } else {
       console.error("Ethereum provider is not available");
     }
   };
   
   setupEventListener();

   // Cleanup the event listener
   return () => {
     if (typeof window.ethereum !== "undefined") {
       const provider = new ethers.BrowserProvider(window.ethereum);
       const contract = new ethers.Contract(contractAddress, abi, provider);
       contract.removeAllListeners("MessageUpdated");
     }
   };
 }, []);

```

This above code sets up an event listener using the useEffect hook to listen for the `MessageUpdated` event emitted by the smart contract whenever the advertisement message is updated.

&#x20;When such an event is detected, it updates the state variables `currentAd`, `currentBid`, and `advertiser` with the new message, advertiser, and bid amount, respectively. This ensures that the displayed data on the web app remains synchronized with the blockchain.

Lastly, it provides a cleanup function to remove the event listener, preventing potential memory leaks when the component is unmounted or re-rendered.

## Code The UI

That’s it, we’re done with the on-chain functionalities, now let’s build UIs to test them out. How you choose to build your UI is entirely up to you, for our project, we’re just going to add the following JSX to our <mark style="color:yellow;">`App.js`</mark> code:

```jsx
<div className="app">
     {/* Landing Section */}
     <section className="landing">
       <h1>BidBoard</h1>
       <p>Status: {status}</p>
     </section>

     <div className="container">
       {/* Bid Section */}
       <section className="bid-section">
         <input
           type="text"
           value={newAd}
           onChange={(e) => setNewAd(e.target.value)}
           placeholder="Enter your advert message"
         />
         <input
           type="number"
           value={bidAmount}
           onChange={(e) => setBidAmount(e.target.value)}
           placeholder="Enter your bid amount"
         />
         <button onClick={submitBid}>Submit Bid</button>
       </section>

       {/* Advert Display Section */}
       <section className="advert-display">
         <div className="current-ad">"{currentAd}"</div>
         <div className="card-details">
           <div className="current-bid">
             Current Bid: <br />
             {currentBid} ETH
           </div>
           <div className="advertiser">
             Advertiser: <br />
             {advertiser}
           </div>
         </div>
       </section>
     </div>

     {/* Footer Section */}
     <footer>
       <a
         href="https://github.com/your-repo"
         target="_blank"
         rel="noopener noreferrer"
       >
         GitHub Repository
       </a>
       {/* Add more links as needed */}
     </footer>
   </div>

```

## Running the project

To run the project open your terminal and run the following command in the project's folder:&#x20;

&#x20;`npm start`

Your console should look similar to this:

<figure><img src="https://lh4.googleusercontent.com/iXPtWgKwS3obTjdvUF_-b88QcBshtDTx66Y2Ayn4ArngJdhehjleB4JQqzuuf0NKuWj0v4p5TPdYvmA674kurL_3VAAx93d903LFiFtdMbACORLUfhL65YFHo9VOzlbz3Ma7QZOvVtTw6oNmSya_SqE" alt="" width="375"><figcaption></figcaption></figure>

Open the URL shown in your browser and you are good to try your dApp!

## Conclusion

This tutorial provided a hands-on journey through creating a web application and connecting it to a smart contract deployed on Mode Testnet using ether.js.&#x20;

Through this project, we delved into essential steps from setting up the development environment to real-time tracking of smart contract events.  You can clone the [code](https://github.com/joshuanwankwo/mode\_testnet) and play around with it!\


To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋

[^1]: 
