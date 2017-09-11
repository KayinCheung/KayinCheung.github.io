# EscrowMyEther
> Open Source Ethereum Smart Contract Dapp that allows 2 transacting parties, a buyer and seller, to trade with their choice of escrow agent.


![](Buyer_Dashboard.png)

## Getting Started

Install Web3 Client:

- Metamask Chrome Extension (https://metamask.io/)
- Parity Chrome Extension (https://chrome.google.com/webstore/detail/parity-ethereum-integrati/himekenlppkgeaoeddcliojfddemadig)

We recommend Metamask as they provide a fully synced Ethereum node. Parity requires you to sync a node and can take a few hours to a few days.
*Make sure to connect to Ropsten test net during beta testing.


## Using the Dapp dashboard

EscrowMyEther has 3 seperate dashboards for buyers, sellers and escrow agents. 
![](Buyer_Dashboard.png)

### Select address
Choose your ethereum address from the dropdown. The dashboard automatically loads your address balance, contract balance (explained below) and your transaction history with the Dapp.

### Understanding contract balance

Contract balances are just like a Paypal balance. Ether in the contract balance belongs to the address and is safely stored in the smart contract.
The address owner can click "Withdraw balance" at any time to withdraw Ether in contract balance to his own address. Just like how Paypal balance is withdrawn to your bank.

Contract balance increases when Ether is transferred to your ownership and there are 3 ways it happens.

Sellers - When a transaction is complete, and the buyer or escrow agent releases funds
Buyers - When seller or escrow agent refunds the buyer
Escrow agents - When the transaction is complete and escrow fee is collected

Contract balance can only be withdrawn to your address. The Dapp does not allow contract balance to be spent on new transactions.

**Update in progress




## Release History

* v1.1	- 10 September 2017
    * EscrowMyEther Contract: 
	  - BuyerFundRelease function now requires refund_approval to be false.
	  - Recompiled with Solidity v0.4.16+commit.d7661dd9
	  - Contract Deployed on Ropsten testnet at https://ropsten.etherscan.io/address/0xe509a834bf9ee3c27af895609e5cdd2f455c4854
	  
* v1.0	- 9 September 2017 
    * Initial commit

## Authors

Cheung Ka Yin – Arrow222 (Reddit)

