# Learn IPFS

## Resources

- [IPFS Camp 2022](https://github.com/ipfs/ipfs-camp-2022)
- [IPFS Tutorial](https://proto.school/)
- [Awesome IPFS](https://github.com/ipfs/awesome-ipfs)


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

## IPFS CLI

Install on Mac

```
brew install ipfs
```

Init

```
ipfs init
```

Run a daemon

```
ipfs daemon
# get id
ipfs id
```

Run web ui

- http://localhost:5001/webui

Get started

```
ipfs cat /ipfs/QmQPeNsJPyVWPFDVHb77w8G42Fvo15z4bG2X8D2GhfbSXc/readme
```

Add a new file to ipfs

```
echo "Hello World" > hello.txt
ipfs add hello.txt
```

View a content with `cat`

```
ipfs cat <CID>
```

Add a directory to ipfs

```
mkdir my_folder
echo "Hello" > my_folder/hello.txt

ipfs add -r my_folder
```

Get detail / view directory

```
ipfs ls <CID>
ipfs ls <CID>/hello.txt
ipfs cat <CID>/hello.txt
```

Get CID of directory without upload to IPFS, this case we can get root CID for a folder and each image inside have own CID, we can set to a nft contract and upload actual image later.

```
// get CID of images folder.
ipfs add --only-hash -r images
```
