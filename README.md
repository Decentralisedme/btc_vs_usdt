# Data Science Capstone Project: Bitcoin vs Tether
This repository contains my Capstone Project completed during General Assembly's Data Science Immersive.

### Introduction to crypto terminology: coins spec
Find as follow basic knowladge and facts about the coins and their realted blockchains:

![image-20200116144849846](/Users/riccardoanacar/Library/Application Support/typora-user-images/image-20200116144849846.png)



### Stablecoins definition

Sstabilise the price of the “coin” by linking its value to

the value of one asset or a pool of assets. We can identify the following

categories:

- Fiat-Backed Stablecoins: Tether
- Crypto-Collateralized Stablecoins: EOSTD / DAI
- Commodities-backed Stablecoins: Digix - Non-Collateralized:

### Project Goal

The aim of the project is to investigate a possible relationship between Tether coin, which is a stable coin paged to the dollar, and the quantity of Bitcoin that has been transacted during the same period

Given the definition of stablecoin itself, USDT is thought to be used as hedging instrument in the following market conditions:

- **High volatility:** stablecoins allow you to transfer assets in a digital eco-system with no exposure to change in values

- **High correlation**: stablecoins allow you to manage your position 
- **Short Term borrowing**

### Data collection

The data are available in the blockchains moreover the ability to commnect to nodes and download the blocks and filter for wanted information have lot of obstacoles, in particular time needed to download the data.

I have to implement different apperaches according to compromise with it:

#### Tether from Ethereum Blockchain:

To interact with any clockchain you need to manage your own node or connect to an existing node which is part of the blockchain.

I connected to Infura node using Web3 python library:

Ss



 

