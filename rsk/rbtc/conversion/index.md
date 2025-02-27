---
layout: rsk
title: Conversion
---

## BTC RBTC Conversion

### Introduction

In this article we will explain step by step on how to convert from BTC to RBTC, and vice versa. The process of conversion is a **2-way peg** mechanism, which locks BTC token on BTC network in BTC-to-RBTC conversion, and releases the BTC token during RBTC-to-BTC conversion.

<div class="fade alert alert-warning show">IMPORTANT: WHITELIST PROCESS. To use the 2-way-peg you must first <a href="/rsk/rbtc/conversion/whitelist">get whitelisted</a>.</div>

## Step by step instructions

You can try the peg process using either a hardware wallet, or using software:

- [Using a Trezor hardware wallet](/rsk/rbtc/conversion/with-trezor)
- [Using a Ledger hardware wallet](/rsk/rbtc/conversion/with-ledger)
- [Using software](/rsk/rbtc/conversion/with-node-and-console)

### Testnet Guide

In this section we will go over the steps of converting BTC to RBTC, and vice versa on the BTC and RBTC testnets.

Note:
The minimum amount of Bitcoin to convert is **0.01 BTC** for Testnet.

#### 1. BTC to RBTC conversion

**1.1 Connect a wallet to BTC testnet**

We recommend to use Electrum BTC wallet for connecting to BTC testnet.

* Download the wallet from [Electrum Website](https://bitzuma.com/posts/a-beginners-guide-to-the-electrum-bitcoin-wallet/)
* Install Electrum
* Start Electrum in testnet mode
  * For example on MacOS:
`/Applications/Electrum.app/Contents/MacOS/Electrum --testnet`
* After Electrum starts, create or import a wallet
* Go to the third tab, "Receive". You will see a Bitcoin Testnet address like below.

![Create a Legacy(P2PK) wallet](/dist/images/legacy-private-key.png)

> Note: The Bitcoin wallet needs to be legacy (not Segwit) whose public key starts with either *m* or *n*, and private key starting with *p2pkh:*

![Get a Bitcoin testnet address in Electrum Wallet](/dist/images/electrum-wallet.png)

**1.2 Get test Bitcoin from testnet Faucet**

There are a few options to get Bitcoin on Testnet. We use [https://testnet-faucet.mempool.co/](https://testnet-faucet.mempool.co/)

**1.3 Whitelist Bitcoin address in RSK**

You can contact us in RSK official [Gitter channels](https://gitter.im/rsksmart/getting-started) to whitelist your Bitcoin testnet address.

**1.4 Send Bitcoin to RSK Federation address**

The Federation address is retrieved by making a Smart Contract call on RSK Testnet. In order to make the call, you will need to have [MyCrypto](https://mycrypto.com/contracts/interact) installed, select RSK Testnet in *"More Networks"*, and Navigate to *"MyCrypto -> Contracts -> Select Existing Contracts -> "Bridge" -> "getFederationAddress"* to execute the call. It should look like the screenshot below.

![Get RSK Federation address from MyCrypto](/dist/images/mycrypto-federation.png)

Once got Federation address, you can send Bitcoin to it from your whitelisted Bitcoin address.

> Note: You need to send a minimum amount of 0.01 BTC for conversion.

**1.5 Get RBTC address with BTC private key**

You can get a corresponding RBTC address with your BTC private key from [https://utils.rsk.co/](https://utils.rsk.co/).

> Note: when entering Bitcoin private key do not include *p2pkh:* in the front.

**1.6 Check RBTC balance on Testnet**

You can check balance of above RBTC address on Metamask, MyCrypto or any RSK testnet compatible wallets.

> Note: You have to wait a minimum of 100 confirmations + a minimum of 5 minutes for checking your RBTC balance

#### 2. RBTC to BTC conversion

**2.1 Get BTC address with RBTC private key**

If you forgot BTC public address you can retrieve it with RSK private key from [https://utils.rsk.co/](https://utils.rsk.co/).


**2.2 Send RBTC to RSK Bridge Contract**

RSK Bridge Contract address: `0x0000000000000000000000000000000001000006`

> Note: The minimum amount to send is 0.005 RBTC for Testnet
Gas Limit of the transaction needs to be manually set at 100,000 gas; otherwise the transaction will fail. Gas Price can be set to 0.06 gwei.

![Customize Gas in Metamask before send transaction on RSK](/dist/images/metamask-gas-limit.png)

**2.3 Check balance of BTC address on Bitcoin Testnet**

You can either use Electrum wallet downloaded earlier or from any Bitcoin explorer to check the balance.
> Note: The release process on Bitcoin network takes 4000 RSK block confirmations and at least 10 more minutes.

### Mainnet Guide

In this section we will go over the steps of converting BTC to RBTC and vice versa in BTC and RBTC mainnet.

Note:
The minimum amount of Bitcoin to convert is **0.01 BTC** for Mainnet.

#### 1. BTC to RBTC conversion

**1.1 Get a BTC address with balance**

Any Bitcoin wallet that supports legacy(P2PK) private key works for this step, and here we recommend to use Electrum BTC wallet for connecting to BTC mainnet.

* Download the wallet from [Electrum Website](https://bitzuma.com/posts/a-beginners-guide-to-the-electrum-bitcoin-wallet/)
* Install Electrum
* Start Electrum
* Once Electrum starts, create or import a wallet
* Go to the third tab "Receive". You will see a Bitcoin Testnet address like below.

> Note: The Bitcoin wallet needs to be legacy (not Segwit) whose public key starts with either *m* or *n*, and private key starting with *p2pkh:*

![Create a Legacy(P2PK) wallet](/dist/images/legacy-private-key.png)

**1.2 Whitelist Bitcoin address in RSK**

You need to complete [whitelisting](/rsk/rbtc/conversion/whitelist).

**1.3 Send Bitcoin to RSK Federation address**

<div class="fade alert alert-warning show">IMPORTANT: DO NOT EXECUTE THIS STEP BEFORE BEING <a href="/rsk/rbtc/conversion/whitelist">WHITELISTED</a>.</div>

<div class="fade alert alert-warning show">Note: You need to send a minimum amount of 0.01 BTC and not more than 10 BTC for conversion.</div>

The Federation address is retrieved by making a Smart Contract call on RSK Mainnet. In order to make the call, you will need to have [MyCrypto](https://mycrypto.com/contracts/interact) installed, select RSK Network, and Navigate to *"MyCrypto -> Contracts -> Select Existing Contracts -> "Bridge" -> "getFederationAddress"* to execute the call. It should look like the screenshot below.

![Get RSK Federation address from MyCrypto](/dist/images/mycrypto-federation.png)

Once you have the Federation address, you can send Bitcoin to it from your whitelisted Bitcoin address.

**1.4 Wait for BTC confirmations**

To ensure the transaction, we need to wait 100 BTC confirmations, be patient :) 

> 100 blocks * 10 minutes/block = 1000 minutes = 16.667 hours approx.

**1.4 Get RBTC address with BTC private key**

You can get a corresponding RBTC address with your BTC private key from [https://utils.rsk.co/](https://utils.rsk.co/).

> Note: when entering Bitcoin private key do not include *p2pkh:* in the front.

**1.5 Check RBTC balance**

You can check balance of RBTC address on Metamask, MyCrypto, or any RSK compatible wallets.

> Note: You have to wait a minimum of 100 confirmations + a minimum of 5 minutes for checking your RBTC balance

#### 2. RBTC to BTC conversion

**2.1 Get BTC address with RBTC private key**

If you forgot BTC public address you can retrieve it with RSK private key from [https://utils.rsk.co/](https://utils.rsk.co/).

**2.2 Send RBTC to RSK Bridge Contract**

RSK Bridge Contract address: `0x0000000000000000000000000000000001000006`

> Note: The minimum amount to send is 0.008 RBTC for Mainnet
Gas Limit of the transaction needs to be manually set at 100,000 gas; otherwise the transaction will fail. Gas Price can be set to 0.06 gwei.

![Customize Gas in Metamask before send transaction on RSK](/dist/images/metamask-gas-limit.png)

**2.3 Check balance of BTC address**

You can either use Electrum wallet downloaded earlier or from any Bitcoin explorer to check the balance.

> Note: The release process on Bitcoin network takes 4000 RSK block confirmations and at least 10 more minutes.

## Video

<div class="video-container">
  <iframe width="949" height="534" src="https://www.youtube-nocookie.com/embed/1jdYVw8zLUg?cc_load_policy=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

### Q & A

**1. How often does the Federation address change?**

Federation address has changed three times since RSK mainnet launch.

**2. Do I lose my Bitcoin if Federation address change during my transfer?**

There is a grace period for Federation address change. You will still be able to lock Bicoin and get RBTC during the grace period, however, any Bitcoin sent to the old Federation address will be lost post to the grace period.

### Feedback

For any questions and suggestions you can post to RSK [Gitter channels](https://gitter.im/rsksmart/getting-started).
