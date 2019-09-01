# Backend API

## fuse-studio-backend v0.1.0

The Fuse Studio REST API for accessing the data and the services of the Fuse network in a simple way. You can use this API to query and interact with the objects of the Fuse network such as: Communities, Tokens, Bridges and Entities.

## Bridge

{% api-method method="get" host="/bridges/:homeTokenAddress" path="" %}
{% api-method-summary %}
Fetch bridge
{% endapi-method-summary %}

{% api-method-description %}
The token bridge connects the Ethereum and Fuse network
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="homeTokenAddress" type="string" required=true %}
Home \(Fuse\) token address
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Token address on the Fuse network
{% endapi-method-response-example-description %}

```aspnet
homeTokenAddress
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Fetch bridge

[Back to top]()

The token bridge connects the Ethereum and Fuse network

```text
GET /bridges/:homeTokenAddress
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| homeTokenAddress | `String` | Home \(Fuse\) token address |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| homeTokenAddress | `String` | Token address on the Fuse network |
| foreignTokenAddress | `String` | Token address on the Ethereum network |
| foreignBridgeAddress | `String` | Bridge address on the Ethereum network |
| homeBridgeAddress | `String` | Bridge address on the Fuse network |
| homeBridgeBlockNumber | `Number` | Bridge creation block number on the Fuse network |
| foreignBridgeBlockNumber | `Number` | Bridge creation block number on the Ethereum network |

## Community

### Add plugins to community

[Back to top]()

```text
POST /communities/:communityAddress
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| communityAddress | `String` | Community address |
| plugins | `Object` | The plugins \(with arguments\) |

#### Param Examples

`json` - Request-Example:

```javascript
{
  "plugins": {
     "businessList": {
         "isActive": true,
      },
     "joinBonus": {
         "isActive": false,
         "hasTransferToFunder": false
     },
  }
}
```

### Fetch community

[Back to top]()

Community is a set of contracts and services. Members of the community are users of the Fuse network. The community is configured via the plugins.

```text
GET /communities/:communityAddress
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| communityAddress | `String` | Community address |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| communityAddress | `String` | Address of the community on the Fuse network |
| homeTokenAddress | `String` | Address of the community token on the Fuse network |
| foreignTokenAddress | `String` | Address of the community token on the Ethereum network |
| homeBridgeAddress | `String` | Address of the community bridge on the Fuse network |
| foreignBridgeAddress | `String` | Address of the community bridge on the Ethereum network |
| isClosed | `Boolean` | Is the community is closed or open. Closed community requires an approve of community admin to join. |
| plugins | `Object` | Defines the community plugins. |

## Entity

### Fetch my communities

[Back to top]()

Fetching communities I'm part of

```text
GET /entities/account/:account
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| account | `String` | address |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| - | `Object[]` | List of entities with their communities and tokens |

### Fetch community entities

[Back to top]()

```text
GET /entities/:communityAddress
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| communityAddress | `String` | Community address of the Fuse network |
| page | `Number` | Page number for pagination |
| withMetadata | `Boolean` | Get entities with entity's metadata |
| search | `String` | Entity's name for a search by name |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| - | `Object[]` | List of entities. See GetEntity endpoint for entity fields |

### Fetch entity

[Back to top]()

Entity is an account on the Fuse network. It can have variety of roles like user, admin, business, or custom defined role.

```text
GET /entities/:communityAddress/:account
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| communityAddress | `String` | Community address |
| account | `String` | Entity's account address |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| account | `String` | Entity's account on Fuse network |
| communityAddress | `String` | Community address of the entity |
| uri | `String` | IPFS URI points to entity's metadata |
| name | `String` | Entity's name |
| roles | `String` | Entity's role encoded as a byte array |
| type | `String` | Entity's type |
| isAdmin | `Boolean` |  |
| isApproved | `Boolean` |  |

## Token

### Fetch token

[Back to top]()

Tokens are compatible with the ERC20 standard, and they also can be burnable/mintable. Tokens are an important part of the community economy.

```text
GET /tokens/:address
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| address | `String` | Token address |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| address | `String` | Token's address |
| name | `String` | Token's name |
| symbol | `String` | Token's symbol |
| tokenURI | `String` | IPFS URI points to token metadata |
| totalSupply | `String` | Token's total supply |
| owner | `String` | Token's owner |
| factoryAddress | `String` | Factory contract that created the token |
| blockNumber | `String` | Block number of the token's creation |
| tokenType | `String` | Token type: basic/mintableBurnable/imported |
| networkType | `String` | Network type where the token is issued: mainnet/ropsten/fuse |

### Fetch tokens

[Back to top]()

```text
GET /tokens
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| networkType | `String` | mainnet/ropsten/fuse |
| page | `Number` | Page number for pagination |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| - | `Object[]` | List of Tokens. See GetToken endpoint for token fields |

### Fetch tokens by owner

[Back to top]()

```text
GET /tokens/owner/:owner
```

#### Parameter Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| owner | `String` | account address of the token owner |
| networkType | `String` | mainnet/ropsten/fuse |

#### Success 200

| Name | Type | Description |
| :--- | :--- | :--- |
| - | `Object[]` | List of Tokens. See GetToken endpoint for token fields |
