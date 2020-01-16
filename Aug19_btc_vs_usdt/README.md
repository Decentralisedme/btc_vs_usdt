# Data Science Capstone Project: Bitcoin vs Tether
This repository contains my Capstone Project completed during General Assembly's Data Science Immersive.

### Introduction to crypto terminology: coins spec
Find as follow basic knowladge and facts about the coins and their realted blockchains:

![image-20200116155329116](/Users/riccardoanacar/Library/Application Support/typora-user-images/image-20200116155329116.png)



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

#### 1 - Tether from Ethereum Blockchain

To interact with any clockchain you need to manage your own node or connect to an existing node which is part of the blockchain.

###### Connect to Infura node using Web3 python library

```python
from web3 import Web3
# CONNECT
web3 = Web3(Web3.HTTPProvider("https://mainnet.infura.io/c4674c2dfb9c4d62b92e662e1ef762db"))
web3.isConnected()
```

######  Filter for Tether transactions: 

Once connected to the node you can retived blocks IDs and their transactions

After putting the Tx numbers in a python list you can filter for the Tether smart contract number 

``` python
# USDC = 0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48
usdt_tx_list =[]
for b in range(0,200):
    for i in range(0, len(tx[b])):
        sc_address = web3.eth.getTransaction(tx[b][i].hex())['to']
         # Tether
        if sc_address =="0xdAC17F958D2ee523a2206206994597C13D831ec7":
            usdt_tx_list.append(tx[b][i])
```

###### Get information about Tether transaction from the Tether transaction number

``` python
usdt_tx_data = []
for row in range(0, len(usdt_tx_list)):
    usdt_tx_data.append(web3.eth.getTransaction(usdt_tx_list[row]))
    #time.sleep(random.normalvariate(3, 0.3))
usdt_tx_data`
```

This step allows us to get inside each Tether transaction and collect its infirmation:

```
AttributeDict({'blockHash': HexBytes('0x2994bdaa2fcd0e1c4d8b854cdb949cb65bdb696ef1243a7df799c8c23ff492d6'),
  'blockNumber': 8962395,
  'from': '0xd8e15C71964B05FFA0884C9Fa21E19F7A3c6449D',
  'gas': 220000,
  'gasPrice': 35000000000,
  'hash': HexBytes('0x38de8c3a68757609dafc4476b3eb9aa9817a67c2ec407668a44a4cfdc967b8e6'),
  'input': '0xa9059cbb0000000000000000000000009138329a251264adbbfe836dc83ac594f862bfe9000000000000000000000000000000000000000000000000000000003b9aca00',
  'nonce': 45857,
  'r': HexBytes('0x527d6d6c0318594528ecbf63ea1d6f3edc1354c3ab8da1448472936cfead5a3e'),
  's': HexBytes('0x2871bbfef1bbd049c0a77c5c082fb1a5d294e54810b89e2dee49bb4e4bb2fafe'),
  'to': '0xdAC17F958D2ee523a2206206994597C13D831ec7',
  'transactionIndex': 6,
  'v': 38,
  'value': 0})
```

#### 2 - Theter Transactions from Google BigQuery

Google BigQuery provides database with Ethereum and Bitcoin blockchian. Here I the query that I wrote to retrive Tether transactions using SQL:

``` sql
SELECT
 *
FROM
 `bigquery-public-data.crypto_ethereum.transactions` AS transactions

WHERE TRUE
 AND transactions.to_address = "0xdac17f958d2ee523a2206206994597c13d831ec7"
 AND transactions.block_timestamp >= "2019-08-01" AND transactions.block_timestamp <= "2019-08-02"
"""```
```

I used similar apprach for Bitcoin

### Predictors
