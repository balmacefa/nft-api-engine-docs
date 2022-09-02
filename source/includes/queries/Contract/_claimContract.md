# POST Claim Collection Contracts
> POST /contract_claims/{testnet || mainnet}/{blockchain:MATIC}

> The above is a response Example:

```json
{
    "id": 4,
    "user": "balmacefa",
    "createdAt": "2022-05-20T07:19:00.690Z",
    "updatedAt": "2022-05-21T16:49:22.986Z",
    "blockchain": "MATIC",
    "useTestNet": false,
    "remainClaims": 9
}
```

<aside class="notice">
POST /contract_claims/{testnet || mainnet}/{blockchain:MATIC}
</aside>

Use this endpoint to claim a collection contract. This depends on your plan.
This endpoint will return the remaining claims to create a new collection contract. 

Please keep in mind that useTestNet refers to either the testnet or the mainnet.

<aside class="warning">
</aside>
🛑You must first call this endpoint before [Create a new NFT](#post-create-nft)🛑
<aside class="warning">
</aside>
