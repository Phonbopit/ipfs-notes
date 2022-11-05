# Learn IPFS


## What is a CID?

> Reference : https://proto.school/anatomy-of-a-cid/01

A CID is a self-describing content-addressed identifier. The number of characters in a CID depends on the **cryptographic hash** of the content. (`sha2-256`)

```
[data or file] --> cryptographic algorithm --> output is fixed size.
```

- **Deterministic** - The same input should always product the same hash.
- **Uncorrelated** - A small change in the input should generate a completely different hash.
- **One-way** - It's impossible to know the data from the hash
- **Unique** - One file can product one hash (can't duplicated)

## Multihash format

A multihash is a self-describing hash which itself contains metadata (length and algorithm). When IPFS was first created, it used `base58btc` encoding. (CIDv0) always start with `Qm...`

---

## How to convert IPFS CIDv0 to CIDv1?

Install

```
npm install multiformats
```


```js
import { CID } from 'multiformats/cid'

export const toV1 = (cidv0: string) => CID.parse(cidv0).toV1().toString()

// example
// toV1('Qm....')
```

