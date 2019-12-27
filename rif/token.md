---
layout: rsk
title: RIF Token
---

<table class="table">
  <tbody>
    <tr>
      <td scope="row">Token Name</td>
      <td>RIF</td>
    </tr>
    <tr>
      <td scope="row">Total Supply</td>
      <td>1,000,000,000 RIF</td>
    </tr>
    <tr>
      <td scope="row">Contract Address</td>
      <td><a href="http://explorer.rsk.co/address/0x2acc95758f8b5f583470ba265eb685a8f45fc9d5" target="_blank">0x2acc95758f8b5f583470ba265eb685a8f45fc9d5</a></td>
    </tr>
    <tr>
      <td scope="row">Contract Type</td>
      <td>ERC677</td>
    </tr>
  </tbody>
</table>

## tRIF (RIF Token in testnet)

<table class="table">
  <tbody>
    <tr>
      <td scope="row">Token Name</td>
      <td>tRIF</td>
    </tr>
    <tr>
      <td scope="row">Total Supply</td>
      <td>1,000,000,000 tRIF</td>
    </tr>
    <tr>
      <td scope="row">Contract Testnet Address</td>
      <td><a href="http://explorer.testnet.rsk.co/address/0x19F64674D8A5B4E652319F5e239eFd3bc969A1fE" target="_blank">0x19F64674D8A5B4E652319F5e239eFd3bc969A1fE</a></td>
    </tr>
    <tr>
      <td scope="row">Contract Type</td>
      <td>ERC677</td>
    </tr>
  </tbody>
</table>

Get tRIF tokens to interact with RNS Testnet variants from the [tRIF faucet](https://faucet.rifos.org).


## ERC677 token standard

An ERC20 token transaction between a regular/non-contract address and contract are two different transactions: You should call approve on the token contract and then call transferFrom on the other contract when you want to deposit your tokens into it.

ERC677 simplifies this requirement and allows using the same transfer function. ERC677 tokens can be sent by calling transfer function on the token contract with no difference if the receiver is a contract or a wallet address, since there is a new way to notify the receive contract of the transfer.

An ERC677 token transfer will be the same as an ERC20 transfer. On the other hand, if the receiver is a contract, then the ERC677 token contract will try to call `tokenFallback` function on receiver contract. If there is no `tokenFallback` function on receiver contract, the transaction will fail.

## RIF transfer methods

- Approve and transfer:
    ```js
    function approve(address _spender, uint256 _value) public returns (bool)
    function transfer(address _to, uint256 _value) public returns (bool)
    ```

- Transfer and call:
    ```js
    function transfer(address _to, uint256 _value, bytes data)
    ```

    **Parameters**
    - `_to: address`: Contract address.
    - `_value: uint256`: Amount of RIF tokens to send.
    - `data: bytes`: 4-byte signature of the function to be executed, followed by the function parameters to be executed with encoded as a byte array.