---
layout: rsk
title: Quick Start - Step 5
---
## Step 5 : Run Smart Contracts

Once the smart contract has been deployed successfully. We can use Truffle console to execute its methods.

Open the truffle console in your terminal using the following command.

```shell
truffle console --network regtest

```

#### Check Balance of Our EIP20 Token

First, let us get the address of the account which was used to deploy the the contract.
We shall save this in the variable `account1`.

```javascript
account1 = (await web3.eth.getAccounts())[0]

```

This should print out an address, similar to `0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826`.
Check that this value matches the first address that you see in Ganache's accounts tab.

Now we can check its balance:

```javascript
EIP20instance = await EIP20.deployed()

await EIP20instance.balanceOf(account1)
```

EIP20 is the name of our contract. This command will print out the balance of the main account as a **big number**, which should appear as `<BN: 2710>`. To see it as an integer:

```javascript
(await EIP20instance.balanceOf(account1)).toNumber()

```

This should appear as `10000`, the number of the tokens was specified in the parameter to the constructor of the smart contract, in the truffle migration.

#### Transfer Token Directly Between Two Accounts

In Ganache, copy the address of the second account in the accounts tab.
We shall save it as a variable, `account2`:

```javascript
account2 = web3.utils.toChecksumAddress('0x2e898C937f22f84a2603fb0BfDeEF43CdAC87f93')

(await EIP20instance.balanceOf(account1)).toNumber()

(await EIP20instance.balanceOf(account2)).toNumber()

```

This should print out `10000` and `0` respectively - all the tokens belong to the first account, and the second account has none.

Next, use the following command to transfer some tokens from the first account to the second account.

```javascript
await EIP20instance.transfer(account2, 10)

```

This should print out an object containing transaction data.

Finally, let us check the account balances to ensure that everything went smoothly:

```javascript
(await EIP20instance.balanceOf(account1)).toNumber()

(await EIP20instance.balanceOf(account2)).toNumber()

```

This should print out `9990` and `10` respectively. The first account has fewer tokens as they have been transferred to the second account.

#### Congratulations

You have reached the end of the quick start tutorials. You are now ready to develop decentralised applications!

----

[Previous](../step4-compile-and-deploy)
