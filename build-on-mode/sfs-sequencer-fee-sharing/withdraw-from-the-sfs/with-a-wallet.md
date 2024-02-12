# With a wallet

To withdraw with a wallet all you have to do is hold the NFT in your wallet and call the withdraw function of the SFS contract directly with your wallet.\
\
To do this, you will need these 3 pieces of information:

* [ ] \_tokenId : This is the ID of your SFS NFT. It's unique and it's incremental by 1 every time someone registers a contract.
* [ ] \_recipient : This is the address to where the earnings will be sent
* [ ] \_amount : this is the amount to withdraw, if you set a higher amount, you will just withdraw the total of the earned fees

Once you have this, you just have to go to [Testnet Blockscout](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=write\_contract) or to [Mainnet Blockscout ](https://explorer.mode.network/address/0x8680CEaBcb9b56913c519c069Add6Bc3494B7020?tab=txs)depending on where your NFT and contracts are delpoyed.

1. Go to the `Contract`  tab and select `Write Contract`&#x20;
2. Look at the bottom for the `11. withdraw` function
3.  Input the toknID, recipient and amount.

    e.g: (203, 0x807CbE33a6F4c0F524C97B2AbcFf919da41cd7Cf, 2342342344)
4. Sign the transaction and wait until you get the rewards!

<figure><img src="../../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>
