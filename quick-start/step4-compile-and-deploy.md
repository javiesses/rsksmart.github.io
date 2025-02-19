---
layout: rsk
title: Quick Start - Step 4
---

<style>
  img.quick-start-step-4{
    margin: 0 auto;
    width: 80%;
  }
</style>

## Step 4 : Compile and Deploy Contracts

Truffle provides a CLI (command line interface) which allows us to easily compile and deploy contracts, including a local blockchain like Ganache.

#### View Contracts and Transactions in Ganache

If you link this Truffle project to Ganache, you will be able to see the contract creation transaction, and contract events in the Ganache GUI app. To link this Truffle project, do the following:

1. Enter Ganache setting screen by clicking the gear icon in the upper right corner
1. Click **Workspace** on the top navigation bar, and then click on **Add Project**
1. Pick the `truffle-config.js` file from `<tutorial-root>/truffle/truffle-config.js`
1. Save and Restart Ganache

<img class="quick-start-step-4" src="/dist/images/add-ganache-1.png" >
<img class="quick-start-step-4" src="/dist/images/add-ganache-2.png" >
<img class="quick-start-step-4" src="/dist/images/add-ganache-3.png" >

#### Compiling Contracts

Change to the root of the truffle directory and then type the following command into a terminal

```shell
cd <tutorial-root>/truffle
npx truffle compile
```

Upon first run, all contracts will be compiled. Upon subsequent runs, Truffle will compile only the contracts that have been changed since the last compile.

Artifacts of the compilation will be placed in the `truffle/build/contracts` directory.


#### Running Migrations

Migrations are JavaScript files that help you deploy contracts to the blockchain network. In this tutorial project, we have already created migration scripts in the migrations folder.

We have previously edited the migration script for the EIP20 token contract (`3_deploy_tokens.js`), which should now look like this:

```javascript
const EIP20 = artifacts.require('./EIP20.sol');

module.exports = (deployer) => {
  deployer.deploy(EIP20, 10000, 'Simon Bucks', 1, 'SBX');
};
```

To run the migrations, run the following command in a terminal

```shell
truffle migrate --reset --network regtest
```

Note that the `--network regtest` parameter tells Truffle to deploy this contract on our local RegNet node.

The migration process may take several minutes depending on the block generation speed. You may want to run it twice to avoid a known issue with Truffle ([#2224](https://github.com/trufflesuite/truffle/issues/2224)).

----

[Previous](../step3-edit-smart-contract)
|
<a href="/quick-start/step5-run-smart-contract" class="green-button">Next</a>