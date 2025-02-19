---
layout: rsk
title: Configuration reference 
---


## Configuration reference
- [peer](#peer)
- [database](#database)
- [vm](#vm)
- [sync](#sync)
- [rpc](#rpc)
- [wallet](#wallet)
- [scoring](#scoring)
- [miner](#miner)
- [blockchain.config.name](#blockchainconfigname)
- [bind_address](#bind_address)
- [public.ip](#publicip)
- [genesis](#genesis)
- [transaction.outdated](#transactionoutdated)
- [play.vm](#playvm)
- [hello.phrase](#phrase)
- [details.inmemory.storage.limit](#detailsinmemorystoragelimit)
- [solc.path](#solcpath)
- [prune](#prune)

## peer
Describes how your node peers other nodes.

* `peer.discovery.enabled = [true/false]` enables the possibility of being discovered by new peers.
* `peer.discovery.ip.list = []` is a list of the peer to start the discovering. These peers must have the `discovery.enabled` option set to true. These are the list of some of RSK bootstrap nodes:

| Network | `ip.list` |
| - | - 
| TestNet |`"bootstrap02.testnet.rsk.co:50505","bootstrap03.testnet.rsk.co:50505","bootstrap04.testnet.rsk.co:50505","bootstrap05.testnet.rsk.co:50505"` | 
| MainNet | `"bootstrap01.rsk.co:5050","bootstrap02.rsk.co:5050","bootstrap03.rsk.co:5050","bootstrap04.rsk.co:5050","bootstrap05.rsk.co:5050","bootstrap06.rsk.co:5050","bootstrap07.rsk.co:5050","bootstrap08.rsk.co:5050","bootstrap09.rsk.co:5050","bootstrap10.rsk.co:5050","bootstrap11.rsk.co:5050","bootstrap12.rsk.co:5050","bootstrap13.rsk.co:5050","bootstrap14.rsk.co:5050","bootstrap15.rsk.co:5050","bootstrap16.rsk.co:5050"` |

* `peer.active = []` is used to connect to specific nodes. It can be empty. 
* `peer.trusted = []` is a list of peers whose incoming connections are always accepted from. It can be empty. 
* `peer.port` is the port used to listen to incoming connections. Default port by each RSK network:

| Network | `peer.port` |
| - | - |
| Regtest | 30305 |
| TestNet | 50505 | 
| MainNet | 5050 |

* `peer.connection.timeout = number (seconds)` defines *in seconds* the timeout for trying to connect to a peer. Suggested value: `2`.
* `channel.read.timeout = number (seconds)` specifies how much time you will wait for a message to come before closing the channel. Suggested value: `30`.
- `peer.privateKey = hash` a securely generated private key unique for your node that **must** be set.
* `peer.networkId = int` is the number of the network to connect to. It's important to mantain these numbers. It identifies the network you are going to connect to. For a regtest private network, you should use always the same (not necessary 34567). RSK networks Ids:

| Network | `peer.networkId` |
| - | - |
| Regtest | 34567 |
| TestNet | 779 |
| MainNet | 775 |


* `peer.maxActivePeers = int` is the max number of active peers that your node will maintain. Suggested value: `30`.

* `peer.p2p.eip8 = bool` forces peer to send handshake message in format defined by [EIP-8](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-8.md).


## database
Describes where the blockchain  database is saved.

* `database.dir = path` is the place to save physical storage files.
* `database.reset = [true/false]
` resets de database when application starts if it is set to *true*.


## vm
Enabling de `vm.structured` will log all the calls to the VM in the local database, this means, all the contract executions (opcodes).
When testing, using this module is the only way to see Exceptions.

* `trace = [true/false]` enables the `vm.structured`.
* `dir = foldername` the directory where calls are saved.
* `compressed = [true/false]` compress data when enabled. 
`initStorageLimit = int` the storage limit.

An example:
```
vm.structured {
    trace = false
    dir = vmtrace
    compressed = true
    initStorageLimit = 10000
}
```

## sync
Options related to syncing the blockchain:
* `sync.enabled = [true/false]` enables the blockchain synchronization. Should be set to `true` to keep the node updated.
* `sync.max.hashes.ask = int` determines the max amount of blocks to sync in a same batch. The synchronization is done in batches of blocks. Suggested value: `10000`.
* `sync.peer.count = int` minimum peers count used in syncing. Sync may use more peers than this value but always trying to get at least this number from discovery. However, it will continue syncing if it's not reached.
* `sync.timeoutWaitingPeers = int (seconds)` timeout to start to wait for syncing requests.
* `sync.timeoutWaitingRequests = int (seconds)` expiration time in minutes for peer status.
* `sync.maxSkeletonChunks = int` maximum amount of chunks included in a skeleton message.
* `sync.shunkSize = int` amount of blocks contained in a chunk, **must be** `192` or a `divisor of 192`.

An example:
```
sync {
    enabled = true
    max.hashes.ask = 10000
    peer.count = 10
    expectedPeers = 5
    timeoutWaitingPeers = 1
    timeoutWaitingRequest = 30
    expirationTimePeerStatus = 10
    maxSkeletonChunks = 20
    chunkSize = 192
}
```

## rpc
Describes the configuration for the RPC protocol.
* `rpc.providers = []` lists the different providers (up to this moment, just `web`). `rpc.providers.web` has a global setting for every web provider, `cors`.
    * `rpc.providers.web.cors = domain` restricts the RPC calls from other domains. Default value is `localhost`.

* `rpc.providers.web` options:
    * `rpc.providers.web.http` defines http configuration:
        * `rpc.providers.web.http.enabled = [true/false]` enables this web provider. Default value is `true`. 
        * `rpc.providers.web.http.port = port` is the HTTP-RPC server listening port. By default RSK uses `4444`.
        * `rpc.providers.web.http.bind_address = address` is the HTTP-RPC server listening interface. By default RSK uses `localhost`.
        * `rpc.providers.web.http.hosts = []` is the list of node's domain names or IPs. Check [restrictions on valid host names](https://en.wikipedia.org/wiki/Hostname#Restrictions_on_valid_host_names).
    * `rpc.providers.web.ws` defines web sockets configuration:
        * `rpc.providers.web.ws.enabled = [true/false]` enables this web provider. Default value is `true`. 
        * `rpc.providers.web.ws.port = port` is the WS-RPC server listening port. By default RSK uses `4445`.
        * `rpc.providers.web.ws.bind_address = address` is the WS-RPC server listening interface. By default RSK uses `localhost`.


* `rpc.modules` lists of different RPC modules. If a module is not in the list and enabled, its RPC calls are discard.
Examples:
```
modules = [
    { name: "eth", version: "1.0", enabled: "true" },
    { name: "net", version: "1.0", enabled: "true" },
    { name: "rpc", version: "1.0", enabled: "true" },
    { name: "web3", version: "1.0", enabled: "true" },
    { name: "evm", version: "1.0", enabled: "true" },
    { name: "sco", version: "1.0", enabled: "true" },
    { name: "txpool", version: "1.0", enabled: "true" },
    { name: "personal", version: "1.0", enabled: "true" }
]
```
It is possible to enable/disable particular methods in a module.
```
{
    name: "evm",
    version: "1.0",
    enabled: "true",
    methods: {
        enabled: ["evm_snapshot", "evm_revert"],
        disabled: [ "evm_reset", "evm_increaseTime"]
    }
}
```
RSK has implemented an RPC [miner module](JSON-RPC-API). To use it, you have to include:
```
{ name: "mnr", version: "1.0", enabled: "true" }
```

## wallet
You can store your accounts on the node to use them to sign transactions. However, it is not secure to use a wallet in a public node.

```
wallet {
    enabled = true
    accounts = [
        {
            "publicKey" : "<PUBLIC_KEY>"
            "privateKey" : "<PRIVATE_KEY>"
        }
    ]
}
```


## scoring
Scoring is the way the node 'punishes' other nodes when bad responses are sent. Punishment can be done by node id or address.
* `scoring.nodes.number = int` number of nodes to keep scoring.
* `scoring.nodes.duration` and `scoring.addresses.duration` initial punishment duration (in minutes). Default is `10`.
* `scoring.nodes.increment` and `scoring.addresses.increment` punishment duration increment (in percentage). Default is `10`.
* `scoring.nodes.maximum` maximum punishment duration (in minutes). Default is `0`.
* `scoring.addresses.maximum` maximum punishment duration (in minutes). Default is `1 week`.

An example:
```
scoring {
    nodes {
        number: 100
        duration: 12
        increment: 10
        maximum: 0
    }
    addresses {
        duration: 12
        increment: 10
        maximum: 6000
    }
}
```
## miner
For more information about configuring RSK node to mine go [here](/rsk/node/configure/for-mining).

## blockchain.config.name
It is a string that describe the name of the configuration.
We use:

| Network | `blockchain.config.name` |
| - | - |
| Regtest | regtest |
| TestNet | testnet |
| MainNet | main |


## bind_address
It's the network interface with *wire protocol* and *peer discovery*.

It is the last resort for public IP when it cannot be obtained by other ways.


## public.ip
It is the node's public IP. If it's not configured, default is the IPv4 returned by `http://checkip.amazonaws.com`. 

## genesis 
It is the path to the genesis file (in *resources/genesis*).
The folder *resources/genesis* contains several versions of genesis configuration according to the network the peer will run on.

| Network | `genesis` |
| - | - |
| Regtest | rsk-dev.json |
| TestNet | bamboo-testnet.json |
| MainNet | rsk-mainnet.json |

## transaction.outdated
It defines when a transaction is outdated: 
* `transaction.outdated.threshold = int` is the number of blocks that should pass before pending transaction is removed. Suggested value: `10`.
* `transaction.outdated.timeout = int` is the number of seconds that should pass before pending transaction is removed. Suggested value: `100` (10 blocks * 10 seconds per block).


## play.vm
It is a boolean that invokes vm program on message received, if the vm is not invoked the balance transfer occurs anyway. Suggested value: `true`.

## hello.phrase
It is a string that will be included in the hello message of the peer.

## details.inmemory.storage.limit
Specifies when exactly to switch managing storage of the account on autonomous db. Suggested value: `1`.
If the inmemory storage of the contract exceded the limit, just deltas are saved.

## solc.path
It is the path to the [Solidity](http://solidity.readthedocs.io) compiler. It's set because you may want to use the node to compile your smart contracts.
If you don't have Solidity installed, you can use `/bin/false` as value.

## prune

The prune service is a process that runs over the node storage to lighten the space it needs to be synchronized. This process removes useless data over a determined amount of blocks processed.

To enable prune service in your node [override your configuration](RSK-node-configuration#setting-your-own-config-preferences). These are the recommended parameters:
```
prune {
    # prune service could be enabled or not
    # values: [true/false]
    # default: false
    enabled = true

    # Number of blocks to process
    blocks {
        # Number of blocks to copy in each prune run
        # default: 5000
        toCopy = 5000

        # Number of blocks to wait to run prune again
        # default: 10000
        toWait = 10000

        # Number of blocks to suspend blockchain process
        # in order to avoid forks
        # default: 100
        toAvoidForks = 100
    }
}
```