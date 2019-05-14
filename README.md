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
* [How the smart contract works](https://github.com/KayinCheung/KayinCheung.github.io#how-the-smart-contract-works)
* [Integrate EscrowMyEther in your site](https://github.com/KayinCheung/KayinCheung.github.io#integration)
* [Changelog](https://github.com/KayinCheung/KayinCheung.github.io#smart-contract-changelog)
* [Known Issues](https://github.com/KayinCheung/KayinCheung.github.io#known-issues)
* [Author](https://github.com/KayinCheung/KayinCheung.github.io#authors)


## Getting Started

Install Ethereum node software:

- [Metamask Chrome Extension](https://metamask.io/)
- [Parity Chrome Extension](https://chrome.google.com/webstore/detail/parity-ethereum-integrati/himekenlppkgeaoeddcliojfddemadig)

We suggest Metamask as they provide a fully synced Ethereum node and only takes 3 mins to setup. Parity requires storing the blockchain locally and takes time to sync your node. Power users may benefit from Parity (such as high volume sellers and escrows), as it loads transaction history quicker.

The Dapp is developed on Google chrome, Parity and Metamask. Other ethereum node and browser combinations may work, but are untested and unsupported.



## Using the dashboard

EscrowMyEther has seperate dashboards for buyers, sellers and escrow agents. 

##### Screenshot of Seller dashboard

![seller_dashboard](https://user-images.githubusercontent.com/24837709/31041944-3efd3520-a5d0-11e7-8f3c-ff5387f6d2b7.jpg)


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

- Notes for Seller (optional)

Fill up the fields and click "proceed to confirmation". Confirm the transaction in your ethereum node and your escrow transaction will be created!

![initialize transaction](https://user-images.githubusercontent.com/24837709/31051404-cfbd440a-a699-11e7-9c97-0f9134f3cdaf.jpg)


Be sure to check that the Seller and Escrow's name and fee is correct. If it shows "Unregistered Seller" or "Unregistered Escrow" make sure to double check.


### 3) Interact with existing transaction
On your dashboard, click on the transaction to view details.

#### Buyers
Buyers can release funds to seller, or raise escrow escalation.

#### Sellers
Sellers can refund the transaction to buyer, or raise escrow escalation.

#### Escrow Agent
When escrow escalation is activated, escrow agents can refund the buyer, or release funds to seller. Escrow escalation can be activated by either the buyer or seller. If escrow escalation is inactive, escrow agents cannot interact with the transaction.

![interact with transaction](https://user-images.githubusercontent.com/24837709/31041943-3ef37698-a5d0-11e7-87bc-f15ca9d95e04.jpg)

## Update profile information
A section to associate a name and information to an ethereum address. Escrow agents also set their fee percentage here, otherwise it default to zero. 

![Update profile](https://user-images.githubusercontent.com/24837709/31041959-8eb9cce0-a5d0-11e7-9e81-db1e4a281225.jpg)

Seller and escrow profile names are shown as buyers create new transactions. When the buyer enters seller address, the seller profile name is displayed in green. Same with escrow address and escrow name.
![modify_profile](https://user-images.githubusercontent.com/24837709/30523431-b56e1bbe-9c13-11e7-9231-6df8e6a742ee.jpg)
If profile name isn't set for the input address, a warning message, "Unregistered Seller" or "Unregistered Escrow" appears in orange.

Buyers can still create new transaction with unregistered sellers and escrows, but please double check with the seller or escrow agent, in case they provided the wrong address. 


## How the smart contract works

When buyers initiate a transaction, 0.25% is taken as dev fee and moved under contract creator's ownership. The remainder 99.75% of funds is locked in the smart contract. If a transaction proceeds smoothly, the buyer can call "buyerFundRelease" with the transaction ID to move ownership of the locked funds (minus escrow fee) to seller. At the same time, escrow fee is moved to escrow's ownership.


Seller can voluntarily refund the buyer by calling "sellerRefund" with sale ID. This moves the funds ownership back to the buyer (minus escrow fees), and the escrow fees under escrow's ownership.


If a dispute happens, either buyer or seller can call "EscrowEscalation". This unlocks the escrow agent's ability to refund the buyer, or release funds to seller. If escrow escalation is not called, the escrow agent has no power to intervene.


Whenever funds are released to seller, or funds are refunded to buyer, the transaction is considered complete. Transaction state will be frozen, any function calls to modify that transaction state will fail.


When funds are transferred to an address's ownership, they are stored in a Funds bank. It's displayed as Contract balance on the Dapp dashboard. These funds can be withdrawn at anytime to the owner's address for spending.

## Integration

Please refer to https://github.com/escrowmyetherbd/escrowmyetherbd.github.io. It's a repository for developers to customize and integrate EscrowMyEther's in other sites. For example if you run a real estate site, you can hard code your address as the escrow agent, and escrow for all transactions on your site.


## Smart Contract Changelog

* v1.2 Mainnet - 28 September 2017
    * Mainnet deployment: 
	  - Escrow Contract: https://etherscan.io/address/0x1c02ce498dc6d0d6ef05a253e021258b07eeba91
	  - Entity Name Storage Contract: https://etherscan.io/address/0xcf356ab67132c1359ebdd0ccc928fdb020eaa929  
	  

* v1.2 Beta - 18 September 2017
    * EscrowMyEther Contract: 
	  - Updated WithdrawFunds function to eliminate chance of re-entrancy attacks.
	  - Fixed critical contract draining bug in escrowDecision.  
	  - No longer fixed to returning 10 transaction history per call. Number can be specified now.	  
	  - Contract Deployed on Ropsten testnet at https://ropsten.etherscan.io/address/0xabd94b3ce2b270d89341d31a1a708b8004436354

* v1.1 Beta - 10 September 2017
    * EscrowMyEther Contract: 
	  - BuyerFundRelease function now requires refund_approval to be false.
	  - Recompiled with Solidity v0.4.16+commit.d7661dd9
	  - Contract Deployed on Ropsten testnet at https://ropsten.etherscan.io/address/0xe509a834bf9ee3c27af895609e5cdd2f455c4854
	  
* v1.0	Beta - 9 September 2017 
    * Initial commit
    
    
## Why EscrowMyEther was created

Transactions over the internet are mostly governed by financial institutions like PayPal and Credit Card companies. With the high lifetime value of Credit Card holders and the lack of alternatives for merchants, financial institutions are inherently biased towards customers when dispute arises.

Lack of competition causes fees to be high. A certain percentage of buyer fraud, transaction fees and currency conversion fees is unavoidable.

These added costs cause a taxation effect, increasing prices for honest customers and reducing profits for merchants. Payment by cryptocurrency solves the issue for merchants, however it provides no protection for buyers if merchants fail to fulfil their obligations. 
    
What’s needed is a transaction method that offer the benefits of cryptocurrency payments, yet has a built in escrow mechanism with fair dispute resolution. 

By creating EscrowMyEther, online transaction methods with escrow protection are not limited to Paypal or financial institutions. Anyone can be the "Paypal" for their community, charge a fee and offer their escrow services. By introducing free market competition, we hope it drives escrow fees down and service levels up, benefiting anyone who transacts online.


## Known Issues 

* Exponential numbers (eg 1e5) are incorrectly considered valid inputs in "Amount to Send [ETH]" input field on new transactions page.

* Refreshing website re-direct users to homepage and occassionally shows "Ethereum Node not connected" despite being connected. 


## Authors

Cheung Ka Yin 

Contact: EscrowMyEther at gmail dot com
