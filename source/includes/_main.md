# Introduction 🤴⚔

This is a fully automated solution 🤖🧞 that allows you to deploy an NFT with a single API call to the [Polygon Matic](https://polygon.technology/) blockchain ( this is a layer 2 Ethereum network). Other blockchains will be added in the future ( BSC, CELO, ONE).


This means that you can now create an NFT and put it on the Polygon blockchain with a single API call. Other blockchains will be added in the future see galaxy use cases 🏰🌈


## Key points 🥇🔑

- Jobs are placed in a resilient Redis queue.
- A smart contract is deployed for each collection.
- Data is uploaded to [IPFS](https://ipfs.io/) (The InterPlanetary File System) in base64 format.
- The IPFS results are included in the NFT Json Metadata.As specified by your custom path. (Internally is done by [lodash _.set](https://lodash.com/docs/4.17.15#set))
- The compiled NFT Json Metadata is uploaded to IPFS.
- The NFT is deployed to the blockchain.
- A webhook is used to notify the user of the job's stages and status.


### The Job queue 💀🥀🧲🧭

The nature of the networks and technology used to create non-fungible tokens (NFTs) means that there are multiple potential points of failure. To account for this, a resilience work queue is used that attempts each step until the NFT is successfully deployed. If a job does not succeed after 10 tries, it is considered unrecoverable.
