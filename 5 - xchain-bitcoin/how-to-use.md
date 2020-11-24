---
sort: 2
---

# How to use

## Installation

```
yarn add @xchainjs/xchain-client
```

Following dependencies will be installed into your project:

- bitcoinjs-lib
- bip39
- wif
- moment
- axios

## Testing

Uses a dotenv file to hold a `USER_PHRASE` and a `VAULT_PHRASE`

## Usage

Initialize client and use class methods:

```
import { Client, Network } from '../src/client'

const btcClient = new Client(Network.TEST)

const newPhrase = btcClient.generatePhrase()
```

### .generatePhrase()

Generate a 12 word BIP-39 seed phrase.

**Return**: `string`

### .setPhrase(`phrase`)

Loads a 12 word BIP-39 seed phrase to use as a BTC send/receive address.

**phrase**: 12 word BIP-39 seed phrase as `string`

**Return**: `void`

### .validatePhrase(`phrase`)

Validates if provided `phrase` is BIP-39.

**phrase**: 12 word BIP-39 seed phrase as `string`

**Return**: `boolean`

### .purgeClient()

Clears UTXOs and seed phrase from client class properties.

**Return**: `void`

### .setNetwork(`net`)

Set testnet or mainnet network using the `Network` interface.

**net**: `Network.TEST` or `Network.MAIN`

**Return**: `void` 

### .setBaseUrl(`endpoint`)

Set an electrs REST API endpoint to use for chain data.

**endpoint**: endpoint as `string`

**Return**: `void` 

### .getAddress()

Gets a P2WPKH address using the seed phrase set in `.setPhrase()` or initialization. If no phrase is set will error.

**Return**: `string` 

### .validateAddress(`address`)

Validates if provided `address` is p2wpkh and same network as the client.

**address**: `string`

**Return**: `boolean` 

### .scanUTXOs()

_Async_

Scans the UTXOs on the set seed phrase in `.setPhrase()` and stores them in class properties.

**Return**: `void` 

### .getBalance()

Get the balance of UTXOs from `.scanUTXOs()`

**Return**: `number` in sats

### .getBalanceForAddress(`address`)

_Async_ 

Get the balance of UTXOs for an external address

**address**: `string`

**Return**: `number` in sats 

### .getTransactions(`address`)

_Async_ 

Get transactions for an address

**address**: `string`

**Return**: `Array` of `objects` 

### .calcFees(`memo`)

_Async_ 

Calculates the fee rate and the fee total estimate for fast, regular, and slow transactions. Add a `memo` for a vault TX

**memo**: `string` _optional_

**Return**: `object` of `objects`

### .vaultTx(`addressVault`, `valueOut`, `memo`, `feeRate`)

_Async_ 

Generates a valid Vault TX hex to be broadcast

**addressVault**: `string`

**valueOut**: `number` in sats

**memo**: `string`

**feeRate**: `number`

### .normalTx(`addressTo`, `valueOut`, `feeRate`)

_Async_ 

Generates a valid Vault TX hex to be broadcast

**addressTo**: `string`

**valueOut**: `number` in sats

**feeRate**: `number`
