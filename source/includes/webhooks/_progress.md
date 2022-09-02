## Progress!! 🤗🏰🍻💥

> This is a progress POST payload example

```json
{
  (...)
  // same as the completed event
  (...)
  "job": {
    "data": {
      "nftMintOrderEntity": {...},
      "nftContractAddress": {...},
      (...)
    (...)
  },
  "workerValue": [
    {
      "topic": "INIT",
      "msg": "NFT Job Started",
      "timestamp": "2022-04-21T21:19:46.192Z"
    },
    {
      "topic": "IPFS",
      "msg": "Uploading to IPFS",
      "timestamp": "2022-04-21T21:19:54.243Z"
    },
    {
      "topic": "IPFS",
      "msg": "Hash: QmVotqYfwe4w5qcnKRmsU8swfWFJmim8uJdwHWEHZau7TW Uploaded to IPFS",
      "timestamp": "2022-04-21T21:20:01.138Z"
    },
    {
      "topic": "IPFS",
      "msg": "IPFS: Uploaded to IPFS",
      "timestamp": "2022-04-21T21:20:01.140Z"
    },
    {
      "msg": "NFT metadata: Building",
      "timestamp": "2022-04-21T21:20:10.891Z"
    },
    {
      "msg": "NFT metadata: Built",
      "timestamp": "2022-04-21T21:20:10.891Z"
    },
    {
      "msg": "NFT metadata: Uploading metadata to IPFS",
      "timestamp": "2022-04-21T21:20:10.914Z"
    },
    {
      "topic": "IPFS",
      "msg": "Uploading to IPFS",
      "timestamp": "2022-04-21T21:20:10.914Z"
    },
    {
      "topic": "IPFS",
      "msg": "Hash: Qma9zdmCq9uh7c8UshsuyKr28mKfWkvjQe1FpWPVzey6jP Uploaded to IPFS",
      "timestamp": "2022-04-21T21:20:27.265Z"
    },
    {
      "msg": "Mint NFT: Init",
      "timestamp": "2022-04-21T21:20:27.400Z"
    },
    {
      "msg": "Mint NFT: Queued",
      "timestamp": "2022-04-21T21:20:29.796Z"
    },
    {
      "msg": "Mint NFT: Waiting for blockchain confirmation",
      "timestamp": "2022-04-21T21:20:29.796Z",
      "count": 1,
      "updatedAt": "2022-04-21T21:20:42.838Z"
    },
    {
      "msg": "Mint NFT: NFT contract created",
      "timestamp": "2022-04-21T21:20:44.492Z"
    },
    {
      "msg": "Mint NFT: Address -> 0xd9a9ff4ae26c6d10b921a79cdfd424e90f758ced694a39a5550423e89e6a4060",
      "data": "0xd9a9ff4ae26c6d10b921a79cdfd424e90f758ced694a39a5550423e89e6a4060",
      "timestamp": "2022-04-21T21:20:44.492Z"
    }
  ],
  "topic": "progress"
}


```
This is triggered when job update the status of the order/job
