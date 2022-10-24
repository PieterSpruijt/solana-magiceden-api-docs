# Solana, MagicEden and other useful api endpoints

Official Magic Eden V2 API docs: [https://api.magiceden.dev/](https://api.magiceden.dev/)

[MagicEden Smart Contract v1](https://solscan.io/account/MEisE1HzehtrDpAAT8PnLHjpSSkRYakotTuJRPjTpo8)

[MagicEden Smart Contract v2](https://solscan.io/account/M2mx93ekt1fmXSVkTrUL9xVFHkmME8HTUi5Cyc5aF7K)

## General Information

[JSON RPC Specification](https://www.jsonrpc.org/specification)

[MongoDB Aggregation Operators](https://www.mongodb.com/docs/manual/reference/operator/aggregation-pipeline/)

### Tested operators

- [$match](https://www.mongodb.com/docs/manual/reference/operator/aggregation/match/)
- [$skip](https://www.mongodb.com/docs/manual/reference/operator/aggregation/skip/)
- [$sort](https://www.mongodb.com/docs/manual/reference/operator/aggregation/sort/)
- [$limit](https://www.mongodb.com/docs/manual/reference/operator/aggregation/limit/)

# Magic Eden RPC Endpoints (https://api-mainnet.magiceden.io/rpc/*)

## Show Current User

Get the details of the currently Authenticated User along with basic
subscription information.

**URL** : `/getNFTByMintAddress/:mintAddress`

**Method** : `GET`

**Auth required** : NO

**CloudFlare** : YES

### _Success Response_

**URL** : `/getNFTByMintAddress/7Y5ZoSVRxzijRocc1w1ycwFws8EcaAKbQgaW1qewfxRy`

**Content examples**

Get a NFT by its Mintaddress

```json
{
  "results": {
    "mintAddress": "7Y5ZoSVRxzijRocc1w1ycwFws8EcaAKbQgaW1qewfxRy",
    "supply": 1,
    "title": "ChicagoBears-Away #6",
    "content": "This is a cute and collectible ChicagoBears SOL NFL Player along with proof of ownership stored on the Solana blockchain",
    "primarySaleHappened": true,
    "updateAuthority": "8sxuMvq8Vi6ynJDLc3vRpzSBk47dRzr98mgozqC1ZovD",
    "onChainCollection": {},
    "sellerFeeBasisPoints": 500,
    "creators": [
      {
        "address": "FWp8BrWxUCs8YahmUmUBpfHczGnMxB87yuXd7m58DrmX",
        "verified": 1,
        "share": 0
      },
      {
        "address": "BLe4ReSFB3GoSxTonTY5D6X9xqudF5NpSP6wL4xJMRau",
        "verified": 0,
        "share": 100
      }
    ],
    "price": 0,
    "owner": "38yGrcoJk8Uec9uQ1vPmztL8mXAH7j12WxEoKU5iJw5y",
    "id": "J9Yusmqch89EQCNayxLKtezKrkC3YXC7fDHzCV6hhwL4",
    "tokenDelegateValid": false,
    "img": "https://www.arweave.net/Vbg6ytjdK0bGsPtgcmcHGo_bF8lyfIN6xOteCDHJsZY?ext=png",
    "attributes": [
      { "trait_type": "Backgrounds", "value": "light Yellow" },
      { "trait_type": "Rarity", "value": "Camp" },
      { "trait_type": "Skin", "value": "Brown" },
      { "trait_type": "Helmet", "value": "NavyBlueOrange" },
      { "trait_type": "Jersey", "value": "White" },
      { "trait_type": "JerseyNo", "value": "49" },
      { "trait_type": "Shinpads", "value": "BlueOrange" },
      { "trait_type": "Shorts", "value": "NavyBlue" },
      { "trait_type": "Socks", "value": "White" },
      { "trait_type": "Shoe", "value": "Silver" },
      { "trait_type": "Uniform", "value": "Away" }
    ],
    "properties": {
      "files": [
        {
          "uri": "https://www.arweave.net/Vbg6ytjdK0bGsPtgcmcHGo_bF8lyfIN6xOteCDHJsZY?ext=png",
          "type": "image/png"
        }
      ],
      "category": "image",
      "creators": [
        {
          "address": "BLe4ReSFB3GoSxTonTY5D6X9xqudF5NpSP6wL4xJMRau",
          "share": 100
        }
      ]
    },
    "propertyCategory": "image",
    "externalURL": "https://www.solnfl.com/",
    "collectionName": "sol_nfl_players",
    "collectionTitle": "SOL NFL PLAYER'S",
    "isTradeable": true
  }
}
```

### Notes

- Make sure the mintaddress is valid and exists on the blockchain

## Get User Bids with query

Get a list of bids with a query for a specific collection

**URL** : `/getBiddingsByQuery`

**Method** : `GET`

**Auth required** : NO

**CloudFlare** : YES

### _Success Response_

**URL** : `/getBiddingsByQuery?q={%20"$match":%20{%20"escrowPubkey":%20"GfhyX9SCkqN5YfQSHvczMxhAFbECiYKHCeHHjL2LbbY5"%20},%20"$sort":%20{%20"createdAt":%20-1%20}%20}`

**Content examples**

**Query** :

```json
{
  "$match": { "escrowPubkey": "GfhyX9SCkqN5YfQSHvczMxhAFbECiYKHCeHHjL2LbbY5" },
  "$sort": { "createdAt": -1 }
}
```

`escrowPubkey` is the public key of the escrow wallet for magic eden

```json
{ "results": [] }
```

For an user that has not made any Bids

### Notes

- Make sure the public key is valid and that the user has made bids before

## Get listed nfts by collection

Get a list of nfts listed for sale by a collection symbol

**URL** : `/getListedNFTsByQuery`

**Method** : `GET`

**Auth required** : NO

**CloudFlare** : YES

### _Success Response_

**URL** : `/getListedNFTsByQuery?q={%22$match%22:{%22collectionSymbol%22:%22cops_game%22},%22$sort%22:{%22createdAt%22:-1},%22$skip%22:0,%22$limit%22:1}`

**Content examples**

**Query** :

```json
{
  "$match": { "collectionSymbol": "cops_game" },
  "$sort": { "createdAt": -1 },
  "$skip": 0,
  "$limit": 1
}
```
`collectionSymbol` is the symbol of the collection


for the collection cops_games

```json
{
  "results": [
    {
      "id": "GworJjYYs9gnS6znuSrPfBMqnB3VLRC4cXh3fFnRSGYT",
      "price": 0.39,
      "escrowPubkey": "77JxCzwDVHiqZ8JZHh3nn1jzkZ4EvN4q2H6JD6sjiufs",
      "owner": "13c2LDGqsaJc5h5FVwKTvnmQndBKsKiMt4L1KjyQeYc5",
      "collectionName": "cops_game",
      "collectionTitle": "Cops Game",
      "img": "https://bafybeidjje4r4sa42ehbciyoqpi45hmzewu7s3bbs4vrtuyvowmeelir3q.ipfs.nftstorage.link/gen3/images/aaf4ac622d77df6ea70e821d946fecfe.png",
      "title": "Cop#44866",
      "content": "Cops Game is a collection of P2E NFT mult-staking game on the Solana blockchain",
      "externalURL": "https://cops.game/",
      "propertyCategory": "image",
      "creators": [
        {
          "address": "A9ajXDuhEsoY7dekvQXdCreawVHkqZy5DJr5XTfxri6m",
          "verified": 1,
          "share": 0
        },
        {
          "address": "MEXuhNRByHZmdL8e9C7nhS9SZ8WrNQ6WeWDWBeEQ8u4",
          "verified": 0,
          "share": 100
        }
      ],
      "sellerFeeBasisPoints": 500,
      "mintAddress": "Fz4K65ZTKExLQKGCguLbDziB9HZz4A97ucjdqQkDndUu",
      "attributes": [
        { "trait_type": "Skin", "value": "Pale White" },
        { "trait_type": "Feet", "value": "Xmas" },
        { "trait_type": "Pants", "value": "Chinos" },
        { "trait_type": "Outfit", "value": "Blue" },
        { "trait_type": "Face", "value": "None" },
        { "trait_type": "Hat", "value": "Bobby" },
        { "trait_type": "Type", "value": "Cop" },
        { "trait_type": "Rank", "value": "Lieutenant" },
        { "trait_type": "Generation", "value": "Gen 3" }
      ],
      "properties": {
        "category": "image",
        "files": [
          {
            "uri": "https://bafybeidjje4r4sa42ehbciyoqpi45hmzewu7s3bbs4vrtuyvowmeelir3q.ipfs.nftstorage.link/gen3/images/aaf4ac622d77df6ea70e821d946fecfe.png",
            "type": "image/png"
          }
        ],
        "creators": [
          {
            "address": "MEXuhNRByHZmdL8e9C7nhS9SZ8WrNQ6WeWDWBeEQ8u4",
            "share": 100
          }
        ]
      },
      "supply": 1,
      "updateAuthority": "MEXuhNRByHZmdL8e9C7nhS9SZ8WrNQ6WeWDWBeEQ8u4",
      "primarySaleHappened": true,
      "onChainCollection": {},
      "isTradeable": true,
      "tokenDelegateValid": false,
      "v2": {
        "auctionHouseKey": "E8cU1WiRWjanGxmn96ewBgk9vPTcL6AEZ1t6F6fkgUWe",
        "sellerReferral": "autMW8SgBkVYeBgqYiTuJZnkvDZMVU2MHJh9Jh7CSQ2",
        "expiry": -1
      },
      "rarity": {
        "merarity": {
          "tokenKey": "Fz4K65ZTKExLQKGCguLbDziB9HZz4A97ucjdqQkDndUu",
          "score": 5.7575144305883986e-12,
          "totalSupply": 49995,
          "rank": 3985
        },
        "moonrank": {
          "rank": 1401,
          "absolute_rarity": 1.4049404554755062e-11,
          "crawl": {
            "id": "cops_game",
            "created": "2022-01-07T14:44:35.401101Z",
            "updated": "2022-10-18T07:13:04.373209Z",
            "first_mint_ts": 1641493170,
            "last_mint_ts": 1646278164,
            "first_mint": "4J2XiwgbJQtqgXt8GdWmQxJUw5Lda5h1kJ7ezZJCxNjY",
            "last_mint": "29ce2tnmmsi7KBiiGFy8jWwx2kjvGSA7NcEmesoRR89q",
            "expected_pieces": 20000,
            "seen_pieces": 17948,
            "last_crawl_id": 1582268495918280700,
            "complete": false,
            "blocked": false,
            "unblock_at_ts": 0
          }
        }
      },
      "createdAt": "2022-10-18T07:45:07.926Z"
    }
  ]
}
```

### Notes

- Make sure the collection has listed nfts

## Get NFTs by owner

Get all NFTs owned by a given address

**URL** : `/getNFTsByOwner/:publicKey`

**Method** : `GET`

**Auth required** : NO

**CloudFlare** : YES

### *Success Response*

**URL** : `/getNFTsByOwner/4nexRvdaGKKSrf9WAFF2mVLSsFiZ4n22ue2kDQzq2MEz`

**Content examples**



```json
{"results":[{"mintAddress":"DKCRpaqdS6DE8b53ao9dFtRYgQ2aw7V2UQqHCsCf9D7J","supply":1,"title":"Solana Walker #542","content":"Just walk on Solana blockchain","primarySaleHappened":true,"updateAuthority":"5D9PXEVJkNcSRBvMmwNtVPknNLQgJqhL3SLjFxyegmkU","onChainCollection":{},"sellerFeeBasisPoints":1500,"creators":[{"address":"7Ps1PcbrUaQoMXmnp7vYfkmu3i9KaEm739D2pcJGw1Us","verified":1,"share":0},{"address":"5D9PXEVJkNcSRBvMmwNtVPknNLQgJqhL3SLjFxyegmkU","verified":0,"share":100}],"price":0,"owner":"4nexRvdaGKKSrf9WAFF2mVLSsFiZ4n22ue2kDQzq2MEz","id":"Dbk8XWD6WiikecGVym27L4x9ikFX2VzZSSZDdxqax3Fh","tokenDelegateValid":false,"img":"https://testlaunchmynft.mypinata.cloud/ipfs/QmXmBdRGwzFfb2HLgnKomcD8e9P6WzBzvfMg22odCUaGbQ/542.gif","attributes":[],"properties":{"files":[{"uri":"https://testlaunchmynft.mypinata.cloud/ipfs/QmXmBdRGwzFfb2HLgnKomcD8e9P6WzBzvfMg22odCUaGbQ/542.gif","type":"image/gif"}],"category":"image","creators":[{"address":"5D9PXEVJkNcSRBvMmwNtVPknNLQgJqhL3SLjFxyegmkU","share":100}]},"propertyCategory":"image","externalURL":"","isTradeable":true}]}
```



### Notes

* Make sure the nfts are on magic eden and that the wallet has nfts

## Get global activities by collection

Get all activities of a given collection, buy, sell, list, delist and bidding history

**URL** : `/getGlobalActivitiesByQuery`

**Method** : `GET`

**Auth required** : NO

**CloudFlare** : YES

### *Success Response*

**URL** : `/getGlobalActivitiesByQuery?q=%7B"%24match"%3A%7B"collection_symbol"%3A"space_runners"%7D%2C"%24sort"%3A%7B"blockTime"%3A-1%2C"createdAt"%3A-1%7D%2C"%24skip"%3A0%7D`

**Content examples**

**Query** :
```json
{"$match":{"collection_symbol":"space_runners"},"$sort":{"blockTime":-1,"createdAt":-1},"$skip":0, "$limit": 10}
```
`collection_symbol` is the collection symbol of the collection you want to get the activities from


```json
{"results":[{"transaction_id":"fLKM5pxFZRDCo5YF4EvrjBvLMVKviP5uveMuu93eqMSG3LxPumobXZcsRVNDgH3TEcqD53icjVuEyia9GQYMUgs","txType":"placeBid","accountKeys":["8ayWVE4EBXPvLYgH9npDyFkEqX4Sfzv54LqVS8W8w9Cu","38HGXnoMgcMR6RXNKenALf47TNafdJWVSfLQsbAxxZog","EfDXngjDX8G7B4oJGQfNcxoVMAt2VgAYzkaJnAgG94cw","11111111111111111111111111111111","3VGM5qiidp62Gmkpp5qfNbFH6ywVN3vTwAnvfhkEdrKY","5f3pEZ1EcJvzcsXS9tbVwLDdmSrQkgzAY1R8QdUSFvKn","autMW8SgBkVYeBgqYiTuJZnkvDZMVU2MHJh9Jh7CSQ2","E8cU1WiRWjanGxmn96ewBgk9vPTcL6AEZ1t6F6fkgUWe","M2mx93ekt1fmXSVkTrUL9xVFHkmME8HTUi5Cyc5aF7K","NTYeYJ1wr4bpM5xo6zx5En44SvJFAd35zTxxNoERYqd","SysvarRent111111111111111111111111111111111","TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA"],"blockTime":1666604101,"buyer_address":"8ayWVE4EBXPvLYgH9npDyFkEqX4Sfzv54LqVS8W8w9Cu","collection_symbol":"space_runners","createdAt":"2022-10-24T09:35:03.922Z","mint":"5f3pEZ1EcJvzcsXS9tbVwLDdmSrQkgzAY1R8QdUSFvKn","notifiable":true,"onChainCollectionAddress":null,"parsedPlacebid":{"TxType":"placeBid","buyer_address":"8ayWVE4EBXPvLYgH9npDyFkEqX4Sfzv54LqVS8W8w9Cu","token_address":"5f3pEZ1EcJvzcsXS9tbVwLDdmSrQkgzAY1R8QdUSFvKn","amount":4100000000,"collection_symbol":"space_runners","mint":"5f3pEZ1EcJvzcsXS9tbVwLDdmSrQkgzAY1R8QdUSFvKn"},"seller_address":null,"signers":["8ayWVE4EBXPvLYgH9npDyFkEqX4Sfzv54LqVS8W8w9Cu"],"slot":157113463,"source":"magiceden_v2","step":0,"totalSteps":1,"txName":"buy","updatedAt":"2022-10-24T09:35:07.690Z","mintObject":{"mintAddress":"5f3pEZ1EcJvzcsXS9tbVwLDdmSrQkgzAY1R8QdUSFvKn","supply":1,"title":"Space Runners x NBA Champions #615","content":"Space Runners is the first NFT Metaverse Fashion brand in collaboration with artists and brands, designing digitally wearable NFTs through Augmented Reality (AR) and plug-in's into the Metaverse as items. \n\nAs the genesis batch, Space Runners teamed up with NBA Champions Kyle Kuzma and Nick Young to launch a 10K Sneaker NFT Collection. Owners of the NFTs become members of an exclusive RUNNERS club, where they can reap members-only benefits such as tickets to NBA basketball games, signed Kyle Kuzma & Nick Young merchandise, exclusive invites to NBA parties & pick up games, auto-whitelist for Space Runners’ next drop, and more.  \n\n🏀Nick Young Sneaker NFT 🏀\n\nVisit www.spacerunners.com for more information.\n","primarySaleHappened":true,"updateAuthority":"4Ls1u7VofB5R66fVgcekVY2REe2s4eNYA7jQHkw6GhMV","onChainCollection":{},"sellerFeeBasisPoints":425,"creators":[{"address":"EAJ6w757boibxSWX9rDy4sbWsqc1tqDc6gnbe8QAGhDd","verified":1,"share":0},{"address":"GF8PMuwqQiLGahuBQkq4eKLndh5D9qGL7p9e3imQkPqR","verified":1,"share":12},{"address":"76FCZeHbqX3ooMyyGfSD3sci1NPCxKhbLro5dF18EJh2","verified":0,"share":44},{"address":"8xgakpq78m29y4o4obkiQ1NHV4vqgxRiuTaXyUmMytdV","verified":0,"share":44}],"img":"https://metadata-temp-api.spacerunners.com/images/615","attributes":[{"trait_type":"Texture","value":"Satin Black"},{"trait_type":"Toes","value":"Four Square"},{"trait_type":"Ankles","value":"Poppers"},{"trait_type":"Laces","value":"XX"},{"trait_type":"Soles","value":"Tan MH Studs"},{"trait_type":"Socks","value":"Loosy Questions"},{"trait_type":"Skin","value":"White"},{"trait_type":"Background","value":"Matte Yellow"}],"properties":{"category":"image","files":[{"uri":"https://metadata-temp-api.spacerunners.com/images/615","type":"image/jpg"}],"creators":[{"address":"EAJ6w757boibxSWX9rDy4sbWsqc1tqDc6gnbe8QAGhDd","verified":true,"share":0},{"address":"GF8PMuwqQiLGahuBQkq4eKLndh5D9qGL7p9e3imQkPqR","verified":false,"share":12},{"address":"76FCZeHbqX3ooMyyGfSD3sci1NPCxKhbLro5dF18EJh2","verified":false,"share":44},{"address":"8xgakpq78m29y4o4obkiQ1NHV4vqgxRiuTaXyUmMytdV","verified":false,"share":44}]},"propertyCategory":"image","externalUrl":"https://spacerunners.com","onChainName":"Space Runners #615","rarity":{"merarity":{"tokenKey":"5f3pEZ1EcJvzcsXS9tbVwLDdmSrQkgzAY1R8QdUSFvKn","score":5.374068162193047e-12,"totalSupply":9806,"rank":1226},"moonrank":{"rank":1215,"absolute_rarity":4.780289930819904e-12,"crawl":{"id":"space_runners","created":"2022-01-04T17:14:16.982267Z","updated":"2022-01-04T17:14:16.982267Z","first_mint_ts":1640225916,"last_mint_ts":1640276032,"first_mint":"Hp2w1FmT3mxeufCZrXBxtsShS5THCNhikvJaKThW2WmY","last_mint":"HBHSLZKw2stX9TB5SutNfC3dTw3D4uGWbkXkZ7nhwjTt","expected_pieces":10000,"seen_pieces":10000,"last_crawl_id":1476700067892039700,"complete":true,"blocked":false,"unblock_at_ts":0}}}}}]}
```


### Notes

* Make sure the collection has a history
