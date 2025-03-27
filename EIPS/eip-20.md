---
eip: 20
title: Token standard
status: Draft
type: Informational
created: 2015-11-19
resolution: https://github.com/ethereum/wiki/wiki/Standardized_Contract_APIs
---

# Abstract

The following describes standard functions a token contract can implement.

# Motivation

Those will allow dapps and wallets to handle tokens across multiple interfaces/dapps.

The most important here are, `transfer`, `balanceOf` and the `Transfer` event.

# Specification

## Token

### Methods

**NOTE**: An important point is that callers should handle `false` from `returns (bool success)`. Callers should not assume that `false` is never returned!

#### totalSupply

``` js
function totalSupply() constant returns (uint256 totalSupply)
```

Get the total token supply

#### balanceOf

``` js
function balanceOf(address _owner) constant returns (uint256 balance)
```

Get the account balance of another account with address `_owner`

#### transfer

``` js
function transfer(address _to, uint256 _value) returns (bool success)
```

Send `_value` amount of tokens to address `_to`

#### transferFrom

``` js
function transferFrom(address _from, address _to, uint256 _value) returns (bool success)
```

Send `_value` amount of tokens from address `_from` to address `_to`

The `transferFrom` method is used for a withdraw workflow, allowing contracts to send tokens on your behalf, for example to "deposit" to a contract address and/or to charge fees in sub-currencies; the command should fail unless the `_from` account has deliberately authorized the sender of the message via some mechanism; we propose these standardized APIs for approval:

#### approve

``` js
function approve(address _spender, uint256 _value) returns (bool success)
```

Allow _spender to withdraw from your account, multiple times, up to the _value amount. If this function is called again it overwrites the current allowance with _value.

#### allowance

``` js
function allowance(address _owner, address _spender) constant returns (uint256 remaining)
```

Returns the amount which `_spender` is still allowed to withdraw from `_owner`

### Events

#### Transfer

``` js
event Transfer(address indexed _from, address indexed _to, uint256 _value)
```

Triggered when tokens are transferred.

#### Approval

``` js
event Approval(address indexed _owner, address indexed _spender, uint256 _value)
```

Triggered whenever `approve(address _spender, uint256 _value)` is called.

# History

Historical links related to this standard:

* Original proposal from Vitalik Buterin: https://github.com/ethereum/wiki/wiki/Standardized_Contract_APIs/499c882f3ec123537fc2fccd57eaa29e6032fe4a
* Reddit discussion: https://www.reddit.com/r/ethereum/comments/3n8fkn/lets_talk_about_the_coin_standard/
