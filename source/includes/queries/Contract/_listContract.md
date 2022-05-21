# List Collection Contracts 🕌📰

> GET /NFT_contracts?{queryParams}
> The above is a response Example:

```json
{
    "data": [
        {
            "id": 18,
            "attributes": {
                "symbol": "ProsperSymbol",
                "blockchain": "MATIC",
                "transactionId": "0xf743b841ce1a5e60229d6cadea5bb8998ccc5c738f7ff0fdf56481d861507c9f",
                "signatureId": "62874642568cff2ddd08ebd1",
                "contractAddress": "0xc40796eCB9583F9dce4fF292408d60FAFBa6e16E",
                "useTestNet": true,
                "createdAt": "2022-05-20T07:24:55.080Z",
                "updatedAt": "2022-05-20T07:42:41.808Z",
                "publishedAt": "2022-05-20T07:24:55.075Z",
                "user": "balmacefa",
                "collectionName": "Prosperity_symbols"
            }
        },
        {...},
        {...}
    ],
    "meta": {
        "pagination": {
            "page": 1,
            "pageSize": 10,
            "pageCount": 1,
            "total": 2
        }
    }
}

```
<aside class="notice">
GET /NFT_contracts?{queryParams}
</aside>


This is endpoint list all collection contracts.
You can use query params to filter the results.

<aside class="warning">
Please consider that `transactionId` is the unique identifier of the NFT in the blockchain.
Use this value to scan and verify the transaction.
</aside>
Example for MATIC Mumbai Testnet:
`transactionId` : 0xf743b841ce1a5e60229d6cadea5bb8998ccc5c738f7ff0fdf56481d861507c9f
[Polygon scan https://mumbai.polygonscan.com/tx/{transactionId}](https://mumbai.polygonscan.com/tx/0xf743b841ce1a5e60229d6cadea5bb8998ccc5c738f7ff0fdf56481d861507c9f)



### Description of query params

| Name | Description |
| ---- | ----------- |
`collectionName` | Name of the collection |
`symbol` | The collection's symbol. For example, the Bitcoin symbol is BTC. |
`blockchain` | The collection's blockchain. For example, MATIC |
`network` | The network of the order [ mainnet / testnet ] |
`page` | The page number of the results. |
`pageSize` | The number of results per page. max: 100 |





