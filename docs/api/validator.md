# web3.ss.stake.validator

The `web3.ss.stake.validator` contains all validator related functions.

---

## declare

```js
web3.ss.stake.validator.declare(validatorToDeclare [, callback])
```

Allows a potential validator declares its candidacy. JSON RPC method: [ss_declareCandidacy].

### Parameters

- `validatorToDeclare`: `Object` - The validator object to declare.

  - `from`: `String` - The address for the sending account. Uses the `web3.ss.defaultAccount` property, if not specified. It will be associated with this validator (for self-staking and in order to get paid).
  - `nonce`: `Number` - (optional) The number of transactions made by the sender prior to this one.
  - `pubKey`: `String` - Validator node public key.
  - `description`: `Object` - (optional) Description object as follows:

    - `name`: `String` - Validator name.
    - `website`: `String` - Web page link.
    - `location`: `String` - Location(network and geo).
    - `email`: `String` - Email.
    - `profile`: `String` - Detailed description.

- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - The block number where the transaction is in. =0 if failed.
  - `hash`: `String` - Hash of the transaction.
  - `check_tx`: `Object` - CheckTx result. Contains error code and log if failed.
  - `deliver_tx`: `Object` - DeliverTx result. Contains error code and log if failed.

### Example

```js
var payload = {
  from: "0xc4abd0339eb8d57087278718986382264244252f",
  pubKey: "051FUvSNJmVL4UiFL7ucBr3TnGqG6a5JgUIgKf4UOIA=",
}
web3.ss.stake.validator.declare(payload, (err, res) => {
  if (!err) {
    console.log(res)
    /*
    {
      check_tx: { fee: {} },
      deliver_tx: {
        "gasUsed": "1000000",
        "fee": {
          "key": "R2FzRmVl",
          "value": "2000000000000000"
        }
      },
      hash: '1573F39376D8C10C6B890861CD25FD0BA917556F',
      height: 271
    }
    */
  } else {
    console.log(err)
    /*
    {
      check_tx: { code: 1, log: 'pubkey has been declared', fee: {} },
      deliver_tx: { fee: {} },
      hash: '032FC10F8B54EBE8028E0ADFD4BB57A9522553D2',
      height: 0
    }
    */
  }
})
```

---

## update

```js
web3.ss.stake.validator.update(validatorToUpdate [, callback])
```

Allows a validator candidate to change its candidacy. JSON RPC method: [ss_updateCandidacy].

### Parameters

- `validatorToUpdate`: `Object` - The validator object to update.

  - `from`: `String` - The address for the sending account. Uses the `web3.ss.defaultAccount` property, if not specified.
  - `nonce`: `Number` - (optional) The number of transactions made by the sender prior to this one.
  - `pubKey`: `String` - (optional) Validator node public key.
  - `description`: `Object` - (optional) When updated, the verified status will set to false:
    - `name`: `String` - Validator name.
    - `website`: `String` - Web page link.
    - `location`: `String` - Location(network and geo).
    - `email`: `String` - Email.
    - `profile`: `String` - Detailed description.

- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - The block number where the transaction is in. =0 if failed.
  - `hash`: `String` - Hash of the transaction.
  - `check_tx`: `Object` - CheckTx result. Contains error code and log if failed.
  - `deliver_tx`: `Object` - DeliverTx result. Contains error code and log if failed.

### Example

```js
var payload = {
  from: "0xc4abd0339eb8d57087278718986382264244252f",
  description: {
    website: "http://www.blahblahblah.com/"
  }
}
web3.ss.stake.validator.update(payload, (err, res) => {
  if (!err) {
    console.log(res)
    /*
    {
      check_tx: { fee: {} },
      deliver_tx: {
        "gasUsed": "1000000",
        "fee": {
          "key": "R2FzRmVl",
          "value": "2000000000000000"
        }
      },
      hash: '1B11C4D5EA9664DB1DD3A9CDD86741D6C8E226E9',
      height: 297
    }
    */
  } else {
    console.log(err)
    /*
    {
      check_tx: { code: 1, log: 'cannot edit non-exsits candidacy', fee: {} },
      deliver_tx: { fee: {} },
      hash: '96E9FAF98075248D69DCC7D0A5697312733D159F',
      height: 0
    }
    */
  }
})
```

---

## withdraw

```js
web3.ss.stake.validator.withdraw(validatorToWithdraw [, callback])
```

Allows a validator to withdraw. JSON RPC method: [ss_withdrawCandidacy].

### Parameters

- `validatorToWithdraw`: `Object` - The validator object to withdraw.

  - `from`: `String` - The address for the validator. Uses the `web3.ss.defaultAccount` property, if not specified.
  - `nonce`: `Number` - (optional) The number of transactions made by the sender prior to this one.

- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - The block number where the transaction is in. =0 if failed.
  - `hash`: `String` - Hash of the transaction.
  - `check_tx`: `Object` - CheckTx result. Contains error code and log if failed.
  - `deliver_tx`: `Object` - DeliverTx result. Contains error code and log if failed.

### Example

```js
var payload = {
  from: "0xc4abd0339eb8d57087278718986382264244252f"
}
web3.ss.stake.validator.withdraw(payload, (err, res) => {
  if (!err) {
    console.log(res)
    /*
    {
      check_tx: { fee: {} },
      deliver_tx: { fee: {} },
      hash: '4A723894821166EFC7DDD4FD92BE8D855B3FDBAC',
      height: 311
    }
    */
  } else {
    console.log(err)
    /*
    {
      check_tx: { code: 1, log: 'cannot withdraw non-exsits candidacy', fee: {} },
      deliver_tx: { fee: {} },
      hash: 'C7AAB80D2F6503CC2BB4CC5843A8361F0D182D6D',
      height: 0
    }
    */
  }
})
```

---

## activate

```js
web3.ss.stake.validator.activate(validatorToActivate [, callback])
```

Allows a "removed" validator to re-activate itself. JSON RPC method: [ss_activateCandidacy].

### Parameters

- `validatorToActivate`: `Object` - The validator object to activate.

  - `from`: `String` - The address for the validator. Uses the `web3.ss.defaultAccount` property, if not specified.
  - `nonce`: `Number` - (optional) The number of transactions made by the sender prior to this one.

- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - The block number where the transaction is in. =0 if failed.
  - `hash`: `String` - Hash of the transaction.
  - `check_tx`: `Object` - CheckTx result. Contains error code and log if failed.
  - `deliver_tx`: `Object` - DeliverTx result. Contains error code and log if failed.

### Example

```js
var payload = {
  from: "0x7eff122b94897ea5b0e2a9abf47b86337fafebdc"
}
web3.ss.stake.validator.activate(payload, (err, res) => {
  if (!err) {
    console.log(res)
    /*
    {
      check_tx: { fee: {} },
      deliver_tx: { fee: {} },
      hash: 'FB70A78AD62A0E0B24194CA951725770B2EFBC0A',
      height: 393
    }
    */
  } else {
    console.log(err)
    /*
    {
      "check_tx": {
        "code": 1,
        "log": "already activated",
        "fee": {}
      },
      deliver_tx: { fee: {} },
      "hash": "FB70A78AD62A0E0B24194CA951725770B2EFBC0A",
      "height": 0
    }
    */
  }
})
```

---

## deactivate

```js
web3.ss.stake.validator.deactivate(validatorToActivate [, callback])
```

Allows a validator to deactivate itself. JSON RPC method: [ss_deactivateCandidacy].

### Parameters

- `validatorToDeactivate`: `Object` - The validator object to deactivate.

  - `from`: `String` - The address for the validator. Uses the `web3.ss.defaultAccount` property, if not specified.
  - `nonce`: `Number` - (optional) The number of transactions made by the sender prior to this one.

- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - The block number where the transaction is in. =0 if failed.
  - `hash`: `String` - Hash of the transaction.
  - `check_tx`: `Object` - CheckTx result. Contains error code and log if failed.
  - `deliver_tx`: `Object` - DeliverTx result. Contains error code and log if failed.

### Example

```js
var payload = {
  from: "0x7eff122b94897ea5b0e2a9abf47b86337fafebdc"
}
web3.ss.stake.validator.deactivate(payload, (err, res) => {
  if (!err) {
    console.log(res)
    /*
    {
      check_tx: { fee: {} },
      deliver_tx: { fee: {} },
      hash: 'FB70A78AD62A0E0B24194CA951725770B2EFBC0A',
      height: 393
    }
    */
  } else {
    console.log(err)
    /*
    {
      "check_tx": {
        "code": 1,
        "log": "already deactivated",
        "fee": {}
      },
      deliver_tx: { fee: {} },
      "hash": "FB70A78AD62A0E0B24194CA951725770B2EFBC0A",
      "height": 0
    }
    */
  }
})
```

---

## updateAccount

```js
web3.ss.stake.validator.updateAccount(updateObject [, callback])
```

A validator requests to update its binding address. JSON RPC method: [ss_updateCandidacyAccount].

### Parameters

- `updateObject`: `Object` - The validator account update object.

  - `from`: `String` - The address for the validator. Uses the `web3.ss.defaultAccount` property, if not specified.
  - `nonce`: `Number` - (optional) The number of transactions made by the sender prior to this one.
  - `newCandidateAccount`: `String` - The new adddress of the validator.

- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - The block number where the transaction is in. =0 if failed.
  - `hash`: `String` - Hash of the transaction.
  - `check_tx`: `Object` - CheckTx result. Contains error code and log if failed.
  - `deliver_tx`: `Object` - DeliverTx result. Contains error code and log if failed. If successful, the requestId will be set in the data property(base64 encoded), for the new address to accept later.

### Example

```js
var payload = {
  from: "0x7eff122b94897ea5b0e2a9abf47b86337fafebdc",
  newCandidateAccount: "0x283ED77f880D87dBdE8721259F80517A38ae5b4f"
}
web3.ss.stake.validator.updateAccount(payload, (err, res) => {
  if (!err) {
    console.log(res)
    /*
    {
      check_tx: { fee: {} },
      deliver_tx: {
        data: "MQ==",
        gasUsed: "1000000",
        fee: { key: "R2FzRmVl", value: "2000000000000000" }
      },
      hash: "34B157D42AFF2D8327FC8CEA8DFFC1E61E9C0D93",
      height: 105
    }
    */
  } else {
    console.log(err)
    /*
    {
      check_tx: { code: 21, log: "Bad request", fee: {} },
      deliver_tx: { fee: {} },
      hash: "ABAAB19BB229404EEF8D62FB9F5FC7C88C595A55",
      height: 0
    }
    */
  }
})
```

---

## acceptAccountUpdate

```js
web3.ss.stake.validator.acceptAccountUpdate(acceptObject [, callback])
```

A validator uses its new address to accept an account updating request. JSON RPC method: [ss_acceptCandidacyAccountUpdate].

### Parameters

- `acceptObject`: `Object` - The accept object.

  - `from`: `String` - The new address for the validator. Uses the `web3.ss.defaultAccount` property, if not specified.
  - `nonce`: `Number` - (optional) The number of transactions made by the sender prior to this one.
  - `accountUpdateRequestId`: `int64` - The account updating request id.

- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - The block number where the transaction is in. =0 if failed.
  - `hash`: `String` - Hash of the transaction.
  - `check_tx`: `Object` - CheckTx result. Contains error code and log if failed.
  - `deliver_tx`: `Object` - DeliverTx result. Contains error code and log if failed.

### Example

```js
var payload = {
  from: "0x283ed77f880d87dbde8721259f80517a38ae5b4f",
  accountUpdateRequestId: 1
}
web3.ss.stake.validator.acceptAccountUpdate(payload, (err, res) => {
  if (!err) {
    console.log(res)
    /*
    {
      check_tx: { fee: {} },
      deliver_tx: {
        gasUsed: "1000000",
        fee: { key: "R2FzRmVl", value: "2000000000000000" }
      },
      hash: "D343D115C152D1A78B7DB9CAA2160E3BA31A3F63",
      height: 67
    }
    */
  } else {
    console.log(err)
    /*
    {
      check_tx: { code: 20, log: "Insufficient bond shares", fee: {} },
      deliver_tx: { fee: {} },
      hash: "D343D115C152D1A78B7DB9CAA2160E3BA31A3F63",
      height: 0
    }
    */
  }
})
```

---

## query

```js
web3.ss.stake.validator.query(validatorAddress [, height] [, callback])
```

Query the current stake status of a specific validator. JSON RPC method: [ss_queryValidator].

### Parameters

- `validatorAddress`: `String` - The validator address.
- `height`: `Number` - (optional) The block number. Default to 0, means current head of the blockchain. NOT IMPLEMENTED YET.
- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - Current block number or the block number if specified.
  - `data`: `Object` - The validator object.

### Example

```js
var info = web3.ss.stake.validator.query("0x7eFf122b94897EA5b0E2A9abf47B86337FAfebdC")
console.log(JSON.stringify(info, null, 2))
/*
{ 
  "height": 38,
  "data": {
    "pub_key": {
      "type": "tendermint/PubKeyEd25519",
      "value": "DuoqmCIcqTzzeBLhz1qt+Q+eCAAHb6bmPng6D1k66Ys="
    },
    "owner_address": "0x7eFf122b94897EA5b0E2A9abf47B86337FAfebdC",
    "shares": "90194330251710238108877",
    "voting_power": 90194,
    "max_shares": "830667891977041679569910",
    "comp_rate": "0.2",
    "created_at": "2018-07-03T10:04:20Z",
    "updated_at": "2018-07-03T14:35:52Z",
    "description": {
      "name": "Sample",
      "website": "https://sample.secondstate.io",
      "location": "CN,ASIA",
      "email": "sample@secondstate.io",
      "profile": "Donec rutrum congue leo eget malesuada. Donec rutrum congue leo eget malesuada. Nulla quis lorem ut libero malesuada feugiat. Donec sollicitudin molestie malesuada. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin eget tortor risus."
    },
    "verified": "N",
    "active": "Y",
    "block_height": 1,
    "rank": 0,
    "state": "Validator"
  }
}
*/
```

---

## list

```js
web3.ss.stake.validator.list([height] [, callback])
```

Returns a list of all current validators and validator candidates. JSON RPC method: [ss_queryValidators].

### Parameters

- `height`: `Number` - (optional) The block number. Default to 0, means current head of the blockchain. NOT IMPLEMENTED YET.
- `callback`: `Function` - (optional) If you pass a callback the HTTP request is made asynchronous. See [this note](https://github.com/ethereum/wiki/wiki/JavaScript-API#using-callbacks) for details.

### Returns

- `Object` - Result object.

  - `height`: `Number` - Current block number or the block number if specified.
  - `data`: `Array` - An array of all current validators and validator candidates. For details of validator object, see [web3.ss.stake.validator.query](#query).

### Example

```js
var info = web3.ss.stake.validator.list()
console.log(JSON.stringify(info, null, 2))
/*
{ 
  "height": 38,
  "data": [
    {
      "pub_key": {
        "type": "tendermint/PubKeyEd25519",
        "value": "DuoqmCIcqTzzeBLhz1qt+Q+eCAAHb6bmPng6D1k66Ys="
      },
      "owner_address": "0x7eFf122b94897EA5b0E2A9abf47B86337FAfebdC",
      "shares": "89884499451603693478569",
      "voting_power": 89884,
      "max_shares": "830667891977041679569910",
      "comp_rate": "0.2",
      "created_at": "2018-07-03T10:04:20Z",
      "updated_at": "2018-07-03T14:35:52Z",
      "description": {
        "name": "Sample",
        "website": "https://sample.secondstate.io",
        "location": "CN,ASIA",
        "email": "sample@secondstate.io",
        "profile": "Donec rutrum congue leo eget malesuada. Donec rutrum congue leo eget malesuada. Nulla quis lorem ut libero malesuada feugiat. Donec sollicitudin molestie malesuada. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin eget tortor risus."
      },
      "verified": "N",
      "active": "Y",
      "block_height": 1,
      "rank": 0,
      "state": "Validator"
    }
  ]
}
*/
```
