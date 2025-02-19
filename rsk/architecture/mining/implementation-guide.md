---
layout: rsk
title: Implementation Guide
---

Here are the steps needed to add RSK merged mining capabilities to mining pool software.

## What do you need to do

Add the RSK merged mining information in Bitcoin block as a commitment, the complete steps are as follow:

### 1. Get the work from RSK node

Use the [mnr_getWork](/develop/json-rpc-api#mnr_getwork) method from the RSK node's JSON-RPC API. This method returns the information of the current block for merged mining, the boundary condition to be met ("target"), and some other data.

### 2. Put the information for merged mining in the Bitcoin block
    
#### Format

`OP_RETURN` + `Length` + `RSKBLOCK:` + `RskBlockInfo`

* `OP_RETURN:` is`0x6a` 
* `Length` is `0x29` and represents the length of the information included after the `OP_RETURN` opcode
* `RSKBLOCK:` is the ascii string for`0x52534b424c4f434b3a` 
* `RskBlockInfo` is the block information in binary format. 

For example, if `RskBlockInfo` is `e5aad3b6b9dc71a3eb98a069bd29ca32211aee8b03fd462f4ffbbe97cc75a174` 
the merged mining information is `6a2952534b424c4f434b3ae5aad3b6b9dc71a3eb98a069bd29ca32211aee8b03fd462f4ffbbe97cc75a174`

#### Position

Include as the last output of Bitcoin coinbase transaction.

#### Restrictions

- The number of bytes immediately after `RskBlockInfo`, up to the end of the coinbase transaction must be lower than or equal to 128 bytes.
- The trailing raw bytes must not contain the binary string `RSKBLOCK:`
- The probability of the RSK tag to appear by chance is negligible, but pool servers must not rule out the possibility of a rogue Bitcoin address included in the coinbase transaction having this pattern, and being used as an attack to break the validity of merged mining header.
- The `RSKBLOCK:` tag may appear by chance or maliciously in the `ExtraNonce2` data field that is provided by miners as part of the Stratum protocol. This is not a problem as long as the poolserver adds the `RSKBLOCK:` tag after the `ExtraNonce2` chunk.

### 3. Notify Miners on a faster pace

RSK average block time is 30 seconds which is faster than Bitcoin 10 minutes. This fact triggers the following implementation changes:

* Retrieve work from RSK node every 2 seconds, so as to be always mining on the last RSK work. 
* Sent to miners a `mining.notify` message, from stratum protocol, every time new RSK work is received.

### 4. Mine until work is enough to meet the target received in the work info

### 5. Submit Solution to RSK node

Use the [mnr_submitBitcoinBlockPartialMerkle](/develop/json-rpc-api#mnr_submitbitcoinblockpartialmerkle) method from RSK node's JSON-RPC API. That method is the optimal in performance and preferred among others available.
Other submission methods and information about the pros and cons between them can be found in the [Mining JSON-RPC API documentation](/develop/json-rpc-api).

## Influence on Bitcoin

As a result of RSK's implementation of merged mining, the Bitcoin network does not get filled up with merged mining information. Only a minimal amount of information is stored: An extra output on the coinbase transaction.

Furthermore, no changes are required on Bitcoin node to support merged mining with RSK.
