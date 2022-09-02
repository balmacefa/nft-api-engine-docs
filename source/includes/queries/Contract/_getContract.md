# GET / Find Collection Contract 🕵🏦🏪

> GET /NFT_contracts/{id || transactionId}

> The above is a response Example:


```json
{
    "symbol": "SYMBOL_0211",
    "blockchain": "MATIC",
    "transactionId": "0x1daf508bc81fbdb26a8713e00295928a2faf4db4dbc1ddff8e0aebea701ad676",
    "signatureId": "6267110dbaca2e7ab8678b03",
    "contractAddress": "0x070d9C506CF0cf31916F0586b76b94ce64478E81",
    "useTestNet": true,
    "createdAt": "2022-04-25T21:22:15.295Z",
    "updatedAt": "2022-04-25T21:23:13.151Z",
    "publishedAt": "2022-04-25T21:22:15.287Z",
    "user": "balmacefa",
    "collectionName": "collection__01s11",
    "id": 17
}
```
<aside class="notice">
GET /NFT_contracts/{id || transactionId}
</aside>

This is endpoint get a collection contract.

You can use the internal id or transaction id to get the collection contract.
The above will return the same result for:

/NFT_contracts/17

/NFT_contracts/ 0x070d9C506CF0cf31916F0586b76b94ce64478E81

<aside class="warning">
Please consider that `transactionId` is the unique identifier of the collection contract in the blockchain.
Use this value to scan and verify the transaction.
</aside>
Example for MATIC Mumbai Testnet:
`transactionId` : 0x070d9C506CF0cf31916F0586b76b94ce64478E81
[Polygon scan https://mumbai.polygonscan.com/tx/{transactionId}](https://mumbai.polygonscan.com/tx/0x070d9C506CF0cf31916F0586b76b94ce64478E81)





