# Hub
- **[Objects](#objects)**

- **[Addresses](#addresses)**
  - **[getNewAddress()](#getnewaddress)**
  - **[getAddress()](#getaddress)**
  - **[isSpent()](#isspent)**

- **[process()](#process)**
  - **[updateBalances()?](#updatebalances)**

- **[sync()](#sync)**

- **[transfer()](#transfer)**
  - **[getInputs()?](#getinputs)**

## Objects:

```
Addresses = [
{
    address: 'W9AZFNWZZZNTAQIOOGYZHKYJHSVMALVTWJSSZDDRVEIXXWPNWEALONZLPQPTCDZRZLHNIHSUKZRSZAZ9W',
    balance: 8500,
    keyIndex: 7,
    security: 2
 }, {
  ...
 }
]
```
TODO - inputs, sweeps, transactions, transfers

## Addresses:
#### `getNewAddress`
Generates a new address from a seed and returns the address.
This address has never been spent from.
##### Inputs
```
getNewAddress(seed, security, checksum)
```
 - **`seed`**: `String` tryte-encoded seed. *seed is never transferred to node
 - **`security`**: `Int`  Security level to be used for the private key / address. _default `constants.SECURITY_LEVEL`_.
 - **`checksum`**: `Bool` Adds 9-tryte address checksum, _default false_.
##### Returns
**`String`** - returns a new address. 

---

#### `getAddress`
Generates an address from the seed and index location.
##### Inputs
```
getAddress(seed, index, security, checksum)
```
 - **`seed`**: `String` tryte-encoded seed. *seed is never transferred to node
 - **`index`**: `Int` key index to derive from seed, 
 - **`security`**: `Int`  Security level to be used for the private key / address. _default `constants.SECURITY_LEVEL`_.
 - **`checksum`**: `Bool` Adds 9-tryte address checksum, _default false_.
##### Returns
**`String`** - returns an address.

---

#### `isSpent`
Checks if an address has ever issued an outgoing transaction.
##### Inputs
```
isSpent(address)
```
 - **`address`**: `String` address to check for.
##### Returns
**`Boolean`** - returns true if an outgoing transaction was ever issued from this address.

---

## Process:
#### `process`
TODO: description
##### Inputs
```
process(seed, inputs, sweeps, addresses, destination, batchSize)
```
 - **`seed`**: `String` tryte-encoded seed. *seed is never transferred to node
 - **`inputs`**: `Array` of input objects, to which received funds will be swept to.
 - **`sweeps`**: `Array` of sweep objects, containing current pending sweeps.
 - **`addresses`**: `Array` of address objects, addresses with balance will be swept.
 - **`destination`**: `String` address to which received funds are swept to, needs to be in `inputs`, _if not provided, the input with the lowest value is selected_.
 - **`batchSize`**: `Int` amount of deposits to sweeps together, _default `constants.MAX_TXS_PER_BUNDLE`_.

##### Returns
**`Sweeps`** - the newly generated sweeps.

---

#### `updateBalances`
updates the `addresses` to reflect the current balance
##### Inputs
```
updateBalances(addresses)
```
 - **`addresses`**: `Array` of address objects
 
##### Returns
**`[addresses]`** a copy of `addresses` with updated balances

---

## Sync:
#### `sync`
TODO: description
##### Inputs
```
sync(inputs, transactions, addresses) 
```
 - **`inputs`**: `Array` of input objects, to update usage status.
 - **`transactions`**: Array` of transaction objects, to check confirmation status
 - **`addresses`**: `Array` of address objects, to scan for balance.

##### Returns
**`[transactions]`** - newly confirmed transactions.

---

## Transfer:
#### `transfer`
TODO: description
##### Inputs
```
transfer(seed, inputs, transfers, options)
```
 - **`seed`**: `String` tryte-encoded seed. *seed is never transferred to node
 - **`inputs`**: `Array` of input objects, used to fund transfer.
 - **`transfers`**: `Array` of transfer objects, specifying the destinations.
 - **`options`**: _optional_

   -**`inputs`**: `Array` of inputs used for funding the transfer
   -**`validateDestination`**: `Boolean` check if destination addresses ever spent funds.
   -**`remainderAddress`**: if defined, this address will be used for sending the remainder   value (of the inputs) to.

##### Returns
**`[Trytes]`** - List of signed trytes, ready to be sent.

---

#### `getInputs`
Get the smallest amount of inputs needed to fund value
##### Inputs
```
getInputs(inputs, value) 
```
 - **`inputs`**: `Array` of inputs used for funding the transfer
 - **`value`**: `Int` total value needed to fund transfer.

##### Returns
**`[inputs]`** - a subset of `inputs`.
