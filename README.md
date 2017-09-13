# EscrowMyEther
Open Source Ethereum Smart Contract Dapp that allows 2 transacting parties, a buyer and seller, to trade with their choice of escrow agent. Website: http://escrowmyether.com/


## Table of contents
* [Getting Started](https://github.com/KayinCheung/KayinCheung.github.io#getting-started)
    * [Using the Dapp dashboard](https://github.com/KayinCheung/KayinCheung.github.io#using-the-dashboard)
    * [Select address](https://github.com/KayinCheung/KayinCheung.github.io#select-address)
    * [Withdrawing contract balance](https://github.com/KayinCheung/KayinCheung.github.io#withdrawing-contract-balance)

* [Initiating new escrow transaction](https://github.com/KayinCheung/KayinCheung.github.io#initiating-new-escrow-transaction)
    * [Finding an escrow agent](https://github.com/KayinCheung/KayinCheung.github.io#1-finding-an-escrow-agent)
    * [Prepare transaction info](https://github.com/KayinCheung/KayinCheung.github.io#2-prepare-transaction-info)
    
* [Interact with existing transaction](https://github.com/KayinCheung/KayinCheung.github.io#3-interact-with-existing-transaction)
    * [Buyer](https://github.com/KayinCheung/KayinCheung.github.io#buyers)
    * [Seller](https://github.com/KayinCheung/KayinCheung.github.io#sellers)
    * [Escrow](https://github.com/KayinCheung/KayinCheung.github.io#escrow-agent)
    
* [Update profile information](https://github.com/KayinCheung/KayinCheung.github.io#update-profile-information)
* [Further questions](https://github.com/KayinCheung/KayinCheung.github.io#further-questions)
* [How the smart contract works](https://github.com/KayinCheung/KayinCheung.github.io#how-the-smart-contract-works)
* [Changelog](https://github.com/KayinCheung/KayinCheung.github.io#smart-contract-changelog)
* [Known Issues](https://github.com/KayinCheung/KayinCheung.github.io#known-issues)
* [Author](https://github.com/KayinCheung/KayinCheung.github.io#authors)


## Getting Started

Install Ethereum node software:

- [Metamask Chrome Extension](https://metamask.io/)
- [Parity Chrome Extension](https://chrome.google.com/webstore/detail/parity-ethereum-integrati/himekenlppkgeaoeddcliojfddemadig)

We recommend Metamask as they provide a fully synced Ethereum node. Parity requires you to sync a node and can take a few hours to a few days. The Dapp is developed on Google chrome, Parity and Metamask. Other ethereum node and browser combinations may work, but are untested and unsupported.

*Make sure to connect to Ropsten test net during beta testing.


## Using the dashboard

EscrowMyEther has seperate dashboards for buyers, sellers and escrow agents. 

##### Screenshot of buyer dashboard

![buyer_dashboard](https://user-images.githubusercontent.com/24837709/30322379-df085308-97eb-11e7-86c7-69daceeca25b.jpg)


### Select address

![select address](https://user-images.githubusercontent.com/24837709/30322994-0dace67c-97ee-11e7-92cf-2623f582a3ff.jpg)

Choose your ethereum address from the dropdown. The dashboard automatically loads your address balance, contract balance, and your transaction history with the Dapp.

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

### 1) Finding an escrow agent

A fair escrow lowers transaction fees and costs associated with buyer fraud for sellers while providing you with buyer protection. If you are buying/selling on a forum, we recommend having a forum moderator to escrow for your transaction. It is important to choose a good escrow agent for your protection. Never use an unknown escrow agent.

### 2) Prepare transaction info

- Seller Address

- Escrow Address

- Amount of Ether to send

Fill up the fields and click "proceed to confirmation". Confirm the transaction in your ethereum node and your escrow transaction will be created!

![initialize transaction](https://user-images.githubusercontent.com/24837709/30327336-43b530b6-97fe-11e7-89ff-8362cf245d85.jpg)


### 3) Interact with existing transaction
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


## How the smart contract works

When buyers initiate a transaction, 0.25% is taken as dev fee and moved under contract creator's ownership. The remainder 99.75% of funds is locked in the smart contract. If a transaction proceeds smoothly, the buyer can call "buyerFundRelease" with the transaction ID to move ownership of the locked funds (minus escrow fee) to seller. At the same time, escrow fee is moved to escrow's ownership.


Seller can voluntarily refund the buyer by calling "sellerRefund" with sale ID. This moves the funds ownership back to the buyer (minus escrow fees), and the escrow fees under escrow's ownership.


If a dispute happens, either buyer or seller can call "EscrowEscalation". This unlocks the escrow agent's ability to refund the buyer, or release funds to seller. If escrow escalation is not called, the escrow agent has no power to intervene.


Whenever funds are released to seller, or funds are refunded to buyer, the transaction is considered complete. Transaction state will be frozen, any function calls to modify that transaction state will fail.


When funds are transferred to an address's ownership, they are stored in a Funds bank. It's displayed as Contract balance on the Dapp dashboard. These funds can be withdrawn at anytime to the owner's address for spending.


## Smart Contract Changelog

* v1.1	- 10 September 2017
    * EscrowMyEther Contract: 
	  - BuyerFundRelease function now requires refund_approval to be false.
	  - Recompiled with Solidity v0.4.16+commit.d7661dd9
	  - Contract Deployed on Ropsten testnet at https://ropsten.etherscan.io/address/0xe509a834bf9ee3c27af895609e5cdd2f455c4854
	  
* v1.0	- 9 September 2017 
    * Initial commit
    
## Website Changelog

I will keep a website changelog after official launch.  Too many updates now.

## Known Issues

* On buyer/seller/escrow dashboards, transaction history gets visually misaligned when toggling next page and previous page. 

* Exponential numbers (eg 1e5) are incorrectly considered valid inputs in "Amount to Send [ETH]" input field.

* Refreshing website re-direct users to homepage and occassionally shows "Ethereum Node not connected" despite being connected. 


## Authors

Cheung Ka Yin – [Arrow222(Reddit)](https://www.reddit.com/user/Arrow222/)

