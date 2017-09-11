# EscrowMyEther
> Open Source Ethereum Smart Contract Dapp that allows 2 transacting parties, a buyer and seller, to trade with their choice of escrow agent.


![](Buyer_Dashboard.png)

## Getting Started

Install Web3 Client:

- Metamask Chrome Extension (https://metamask.io/)
- Parity Chrome Extension (https://chrome.google.com/webstore/detail/parity-ethereum-integrati/himekenlppkgeaoeddcliojfddemadig)

We recommend Metamask as they provide a fully synced Ethereum node. Parity requires you to sync a node and can take a few hours to a few days. The Dapp is developed on Google chrome, Parity and Metamask. Other ethereum node and browser combinations may work, but are untested and unsupported.

*Make sure to connect to Ropsten test net during beta testing.


## Using the Dapp dashboard

EscrowMyEther has seperate dashboards for buyers, sellers and escrow agents. 
![](Buyer_Dashboard.png)

### Select address
Choose your ethereum address from the dropdown. The dashboard automatically loads your address balance, contract balance (explained below) and your transaction history with the Dapp.

### Withdrawing contract balance

Contract balances are like a Paypal balance. Ether in the contract balance belongs to the address and is safely stored in the smart contract.
The address owner can click "Withdraw balance" at any time to withdraw Ether in contract balance to his own address. Just like how Paypal balance is withdrawn to your bank.

When Ether is transferred to your ownership, it is added to your contract balance. It can happen in 3 ways.

Sellers - When the buyer or escrow agent releases funds

Buyers - When seller or escrow agent refunds the buyer

Escrow agents - When the transaction is complete and escrow fee is collected

Contract balance can only be withdrawn to your address. The Dapp does not allow contract balance to be spent on new transactions.


## Initiating new escrow transaction

A new escrow transaction can be created by clicking "Initialize new transaction" under buyer dashboard. 

### 1) Reach an agreement with the seller on the escrow agent for your transaction.

A fair escrow lowers transaction fees and costs associated with buyer fraud for sellers while providing you with buyer protection. If you are buying/selling on a forum, we recommend having a forum moderator to escrow for your transaction. It is important to choose a good escrow agent for your protection. Never use an unknown escrow agent.

### 2) Have the following info at hand

- Seller Address

- Escrow Address

- Amount of Ether to send

Fill up the fields and click "proceed to confirmation". Confirm the transaction in your ethereum node and your escrow transaction will be created!

### 3) Interacting with a transaction
Enter the transaction ID here and click one of the two buttons to interact with the transaction.

#### Buyers
Buyers can release funds to seller, or raise escrow escalation.

#### Sellers
Sellers can refund the transaction to buyer, or raise escrow escalation.

#### Escrow Agent
When escrow escalation is activated, escrow agents can refund the buyer, or release funds to seller. Escrow escalation can be activated by either the buyer or seller. If escrow escalation is inactive, escrow agents cannot interact with the transaction.


## Update profile information
A section to associate a name and information to an ethereum address. Escrow agents can also set their fee percentage here, otherwise it default to zero. There are plans to integrate these information in the Dapp and to build a search function in the future. For now this feature is largely unused, except for setting escrow fees.


## Further questions
Feel free to post your questions on our subreddit forum, send a pm on reddit or raise an issue on github.


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

