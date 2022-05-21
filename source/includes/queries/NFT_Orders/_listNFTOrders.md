# GET List NFT Orders 📜📄

> GET /NFT_orders?{queryParams}

> The above is a response Example:

```json
{
   "data":[
      {
         "id":41,
         "attributes":{
            "sendAddress":"0xf2b5b9e978ee841c2b1507a09aa715d19f0d76fc",
            "blockchain":"MATIC",
            "collectionName":"Prosperity_symbols",
            "symbol":"ProsperSymbol",
            "tokenId":"1",
            "royalties":[
               {
                  "address":"0x1837F49559fC820f28C1C239aDF53854dba570Ba",
                  "splitRoyaltyRate":10
               }
            ],
            "rapidApiRequestHeaders":{
               
            },
            "nftMetadata":{
               "description":"The Jin Chan is a mythical creature that is said to appear during the full moon, near houses or businesses that will soon receive good news. Most of the time, the nature of this good news is understood to be wealth-related.  According to feng shui beliefs, Jin Chan helps attract and protect wealth, and guards against bad luck.",
               "image":"ipfs://QmNxndGHmVnj31ikQxaFEdBEPQgLnuR1ANYuJtE5DFrMhM",
               "name":"Jin Chan",
               "attributes":[
                  {
                     "trait_type":"Species",
                     "value":"Toad"
                  },
                  {
                     "trait_type":"Ability",
                     "value":"Attracts and protects wealth, and guards against bad luck"
                  },
                  {
                     "trait_type":"Weakness",
                     "value":"Should never be kept in the bathroom, bedroom, dining room or kitchen"
                  },
                  {
                     "display_type":"date",
                     "trait_type":"birthday",
                     "value":1546360800
                  }
               ],
               "custom_data":{
                  "wikepedia":"https://en.wikipedia.org/wiki/Jin_Chan"
               }
            },
            "nftMetadataIPFS":"ipfs://QmeFZNfD8NMLoDPteiqw7pyNCyriUzSgHaygEkZgak4TMj",
            "transactionId":"0xc9ebb4936de7fb986123336d1034c0e452ae0baa6913947f503ece55c986114a",
            "signatureId":"628746854f1b6fc2e332a761",
            "contractAddress":"0xc40796eCB9583F9dce4fF292408d60FAFBa6e16E",
            "status":"minted",
            "user":"balmacefa",
            "createdAt":"2022-05-20T07:24:47.678Z",
            "updatedAt":"2022-05-21T01:49:05.355Z",
            "useTestNet":true
         }
      },
      {...},
      {...},
   ],
   "meta":{
      "pagination":{
         "page":1,
         "pageSize":10,
         "pageCount":1,
         "total":3
      }
   }
}

```
<aside class="notice">
GET /NFT_orders?{queryParams}
</aside>


This is endpoint list all NFT orders.
You can use query params to filter the results.

<aside class="warning">
Please consider that `transactionId` is the unique identifier of the NFT in the blockchain.
Use this value to scan and verify the transaction.
</aside>
Example for MATIC Mumbai Testnet:
`transactionId` : 0xc9ebb4936de7fb986123336d1034c0e452ae0baa6913947f503ece55c986114a
[Polygon scan https://mumbai.polygonscan.com/tx/{transactionId}](https://mumbai.polygonscan.com/tx/0xc9ebb4936de7fb986123336d1034c0e452ae0baa6913947f503ece55c986114a)



### Description of query params

| Name | Description |
| ---- | ----------- |
`contractAddress` | The address of the contract that issued the NFT. |
`status` | The status of the order in the job-queue [ pending / minted / failed ] |
`network` | The network of the order [ mainnet / testnet ] |
`page` | The page number of the results. |
`pageSize` | The number of results per page. max: 100 |





