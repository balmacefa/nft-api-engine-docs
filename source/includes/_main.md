
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

# Create NFT 🌈📜

> The above is a payload Example:

```json
{
  "nftMintOrder": {
    "sendAddress": "0xf2B5B9E978Ee841c2b1507a09Aa715D19F0D76fc",
    "blockchain": "MATIC",
    "tokenId": "1",
    "collectionName": "collection__01",
    "symbol": "SYMBOL_01",
    "royalties": [
      {
        "address": "0x1837F49559fC820f28C1C239aDF53854dba570Ba",
        "splitRoyaltyRate": 10
      }
    ]
  },
  "nftMetadata": {
    "description": "See opensea standard - https://docs.opensea.io/docs/metadata-standards",
    "external_url": "https://your_domain.xyz/nft/1",
    "image": "This will be set by payload: uploadIpfsFiles[0].setMetadataPath",
    "animation_url": "uploadIpfsFiles[1].setMetadataPath ??",
    "name": "Name of the NFT -- see standards ^^",
    "attributes": [
      {
        "trait_type": "Personality",
        "value": "Go4It"
      },
      {
        "display_type": "date",
        "trait_type": "birthday",
        "value": 1546360800
      }
    ],
    "custom_data": {
      "key": "You can set any property outside the marketplace standards"
    }
  },
  "webhooks": {
    "completed": "https://your_domain.xyz/completed",
    "progress": "https://your_domain.xyz/progress",
    "failed": "https://your_domain.xyz/failed",
    "unrecoverableFatalError": "https://your_domain.xyz/unrecoverableFatalError"
  },
  "uploadIpfsFiles": [
    {
      "setMetadataPath": "image",
      "base64data": "AAIAAAAEAI.... gg_> encoded 64 data nodejs; .json, .png to  base64 data nodejs  ....FDAAA94N0="
    }
  ]
}

```

</br>
> This is the Payload JSON Schema:

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "description": "A JSON schema for: Create NFT in one API call",
  "properties": {
    "nftMintOrder": {
      "type": "object",
      "description": "This defines the NFT Collection - Blockchain, collection name, royalties, symbol, and the Unique NFT Token id; this information is used to identify the order in the system.",
      "properties": {
        "sendAddress": {
          "type": "string",
          "description": "During the Mint phase, the NFT will be sent to this address. This will be the NFT's owner."
        },
        "blockchain": {
          "type": "string",
          "description": "At the moment, only Polygon MATIC is supported. Other blockchains will be integrated in the future ( BSC, CELO, ONE).",
          "enum": [
            "MATIC"
          ]
        },
        "tokenId": {
          "type": "string",
          "description": "Token ID that will be issued. This identifies the NFT within the collection.",
          "pattern": "^[0-9]{1,32}$"
        },
        "collectionName": {
          "type": "string",
          "description": "Name of the collection"
        },
        "symbol": {
          "type": "string",
          "description": "The collection's symbol. For example, the Bitcoin symbol is BTC.",
          "pattern": "^[a-zA-Z0-9_-]{1,30}$"
        },
        "royalties": {
          "type": "array",
          "description": "At the moment, Opensea does not support split revenue. When a splitter address is implemented or our NFT Marketplace contract becomes accessible, this information will be used. This project will earn a split revenue of 2.5%.",
          "items": [
            {
              "type": "object",
              "properties": {
                "address": {
                  "type": "string",
                  "description": "Address where royalties should be sent every transaction"
                },
                "splitRoyaltyRate": {
                  "type": "number",
                  "description": "Percentage for this Address"
                }
              },
              "additionalProperties": false,
              "required": [
                "address",
                "splitRoyaltyRate"
              ]
            }
          ],
          "additionalItems": true
        }
      },
      "additionalProperties": false,
      "required": [
        "sendAddress",
        "blockchain",
        "tokenId",
        "collectionName",
        "symbol"
      ]
    },
    "nftMetadata": {
      "type": "object",
      "description": "NFT JSON Metadata, This can be a NFT standard or any other structure that fits your business logic. For Opensea or marketplace standard see https://docs.opensea.io/docs/metadata-standards",
      "additionalProperties": true
    },
    "webhooks": {
      "type": "object",
      "description": "Webhook for each stage of the redis job status - For further information and structure, see the Webhooks Section.",
      "properties": {
        "completed": {
          "type": "string",
          "description": "This is triggered when the NFT is successfully minted."
        },
        "progress": {
          "type": "string",
          "description": "This is triggered when job update the status of the order/job"
        },
        "failed": {
          "type": "string",
          "description": "This is triggered when a task fails. Please keep in mind that the job is retrying 10 times until the order's status is declared as unrecoverable. Fatal Error"
        },
        "unrecoverableFatalError": {
          "type": "string",
          "description": "This is triggered when a job fails many times and will not be retried; the job is then removed from the queue stack."
        }
      },
      "additionalProperties": false,
      "required": [
        "completed"
      ]
    }
  },
  "uploadIpfsFiles": {
    "type": "array",
    "description": "A collection of base64 data to be uploaded to the IPFS. Also, assign each file result to the NFT Metadata Path.",
    "items": [
      {
        "type": "object",
        "properties": {
          "base64data": {
            "type": "string",
            "description": "Base 64 data will be uploaded to the IPFS."
          },
          "setMetadataPath": {
            "type": "string",
            "description": "The upload result will be set to JSON NFT Metadata obj, specify by this Path, which is done internally by  [lodash _.set](https://lodash.com/docs/4.17.15#set)"
          }
        },
        "additionalProperties": false,
        "required": [
          "base64data",
          "setMetadataPath"
        ]
      }
    ],
    "additionalItems": true
  },
  "additionalProperties": false,
  "required": [
    "nftMintOrder",
    "nftMetadata"
  ]
}

```


Use this endpoint to deploy and NFT.
This is a fully automated solution 🤖🧞 that allows you to deploy an NFT with a single API call to the [Polygon Matic](https://polygon.technology/) blockchain ( this is a layer 2 Ethereum network). Other blockchains will be added in the future ( BSC, CELO, ONE).

<aside class="notice">
Please review the JSON Schema for this endpoint.
</aside>
<p>
</p>

### Payload Properties 💣💥
 - <b id="#/properties/nftMintOrder">🔸 nftMintOrder</b> Type: `object` | `⛑ required`
   <p>
   _This defines the NFT Collection - Blockchain, collection name, royalties, symbol, and the Unique NFT Token id; this information is used to identify the order in the system._
   This schema <u>does not</u> accept additional properties.
   </p>
**_Properties:::_**
  - <b id="#/properties/nftMintOrder/properties/sendAddress">🔸 sendAddress</b> Type: `string` | `⛑ required`
    <p>
    _During the Mint phase, the NFT will be sent to this address. This will be the NFT's owner._
    </p>

  - <b id="#/properties/nftMintOrder/properties/blockchain">🔸 blockchain</b> Type: `string` | `⛑ required`
    <p>
    _At the moment, only Polygon MATIC is supported. Other blockchains will be integrated in the future ( BSC, CELO, ONE)._
    </p>
    <p>
    The value is restricted to the following: 
      1. _"MATIC"_
    </p>
  - <b id="#/properties/nftMintOrder/properties/tokenId">🔸 tokenId</b> Type: `string` | `⛑ required`
    <p>
    _Token ID that will be issued. This identifies the NFT within the collection._
    </p>
    <p>
    The value must match this pattern: `^[0-9]{1,32}$`
    </p>

  - <b id="#/properties/nftMintOrder/properties/collectionName">🔸 collectionName</b> Type: `string` | `⛑ required`
    <p>
    _Name of the collection_
    </p>

  - <b id="#/properties/nftMintOrder/properties/symbol">🔸 symbol</b> Type: `string` | `⛑ required`
    <p>
    _The collection's symbol. For example, the Bitcoin symbol is BTC._
    </p>
    <p>
        The value must match this pattern: `^[a-zA-Z0-9_-]{1,30}$`
    </p>

  - <b id="#/properties/nftMintOrder/properties/royalties">🔸 royalties</b> Type: `array`
    <p>
    _At the moment, Opensea does not support split revenue. When a splitter address is implemented or our NFT Marketplace contract becomes accessible, this information will be used. This project will earn a split revenue of 2.5%._
    </p>
      - <b id="#/properties/nftMintOrder/properties/royalties/items">**_Items_**</b> Type: `object`
        <p>
        This schema <u>does not</u> accept additional properties.
        </p>
        <p>
        **_Properties:::_**
        </p>
        - <b id="#/properties/nftMintOrder/properties/royalties/items/properties/address">🔸 address</b> Type: `string` | `⛑ required`
          </p>
          _Address where royalties should be sent every transaction_
          <p>

        - <b id="#/properties/nftMintOrder/properties/royalties/items/properties/splitRoyaltyRate">🔸 splitRoyaltyRate</b> Type: `number` | `⛑ required`
          </p>
          _Percentage for this Address_
          <p>

 - <b id="#/properties/webhooks">🔸 webhooks</b> Type: `object`
    </p>
    _Webhook for each stage of the redis job status - For further information and structure, see the Webhooks Section._
    <p>
    This schema <u>does not</u> accept additional properties.
    </p>
    <p>
    **_Properties:::_**
     - <b id="#/properties/webhooks/properties/completed">🔸 completed</b> Type: `string` | `⛑ required`
        <p>
        _This is triggered when the NFT is successfully minted._
        </p>

     - <b id="#/properties/webhooks/properties/progress">🔸 progress</b> Type: `string`
        <p>
        _This is triggered when job update the status of the order/job_
        </p>

     - <b id="#/properties/webhooks/properties/failed">🔸 failed</b> Type: `string`
        <p>
        _This is triggered when a task fails. Please keep in mind that the job is retrying 10 times until the order's status is declared as unrecoverable. Fatal Error_
        </p>

     - <b id="#/properties/webhooks/properties/unrecoverableFatalError">🔸 unrecoverableFatalError</b> Type: `string`
      <p>
      _This is triggered when a job fails many times and will not be retried; the job is then removed from the queue stack._
      </p>

 - <b id="#/properties/uploadIpfsFiles">🔸 uploadIpfsFiles</b> Type: `array`
    <p>
    _A collection of base64 data to be uploaded to the IPFS. Also, assign each file result to the NFT Metadata Path._
    </p>
    <p>
    This schema <u>does not</u> accept additional items.
    </p>
      - <b id="#/properties/nftMintOrder/properties/royalties/items">**_Items_**</b> Type: `object`
        <p>
        This schema <u>does not</u> accept additional properties.
        </p>
        
        **_Properties:::_**
       - <b id="#/properties/uploadIpfsFiles/items/properties/base64data">🔸 base64data</b> Type: `string` | `⛑ required`
          <p>
          _Base 64 data will be uploaded to the IPFS._
          </p>

       - <b id="#/properties/uploadIpfsFiles/items/properties/setMetadataPath">🔸 setMetadataPath</b> Type: `string` | `⛑ required`
          <p>
          _The upload result will be set to JSON NFT Metadata obj, specify by this Path, which is done internally by  [lodash _.set](https://lodash.com/docs/4.17.15#set)_
          </p>
