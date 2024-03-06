---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Registration

{% hint style="danger" %}
To register your contact you need to do some code changes so please check [register-a-smart-contract](../../build-on-mode/sfs-sequencer-fee-sharing/register-a-smart-contract/ "mention") before deploying your final version.
{% endhint %}

## What does registering a contract mean?

Registering a contract in the SFS means calling the <mark style="color:orange;">`register`</mark>  register defined in the SFS contract and getting an SFS NFT in exchange. The call to the register function must be made from your smart contract. This means you will have to add some code and logic to your contract in order to register it to the SFS. You’ll find code to do this later on this guide.

This is the register function from the SFS:

{% code lineNumbers="true" fullWidth="true" %}
```solidity
    ///@notice Mints ownership NFT that allows the owner to collect fees earned by the smart contract.
        ///`msg.sender` is assumed to be a smart contract that earns fees. Only smart       ///contract itself can register a fee receipient.
    /// @param _recipient recipient of the ownership NFT
    /// @return tokenId of the ownership NFT that collects fees
    function register(address _recipient) public onlyUnregistered returns (uint256 tokenId) {
        address smartContract = msg.sender;

        if (_recipient == address(0)) revert InvalidRecipient();

        tokenId = _tokenIdTracker.current();
        _mint(_recipient, tokenId);
        _tokenIdTracker.increment();

        emit Register(smartContract, _recipient, tokenId);

        feeRecipient[smartContract] = NftData({
            tokenId: tokenId,
            registered: true,
            balanceUpdatedBlock: block.number
        });
    }
```
{% endcode %}

There are 2 interesting things to note from the register function:

1. The register function receives (<mark style="color:red;">`address`</mark>` ``_recipient`) as a parameter. This is the address where the NFT will be minted to.&#x20;
2. The SFS contract looks at the <mark style="color:orange;">`msg.sender`</mark> in order to know what smart contract is being registered. This is why you need to call the register function from the contract you want to register. **You can only do this once per contract.**

