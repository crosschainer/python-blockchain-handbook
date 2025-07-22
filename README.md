# Python Smart Contracts: Ecosystem Overview

Smart contracts are self-executing programs on blockchain networks that enable decentralized applications and automated agreements without intermediaries. Python’s clear syntax and extensive libraries make it a popular choice for writing, testing, and auditing smart contracts across multiple platforms. Different ecosystems leverage Python in various ways—from Python-like contract languages that compile down to blockchain bytecode, to native execution of Python code on a blockchain. This overview covers four major Python-centric smart contract approaches: **Vyper** (Ethereum), **PyTeal** (Algorand), **SmartPy** (Tezos), and **[XIAN](https://xian.org)** (a native-Python Layer-1).

## Frameworks & Languages

### Vyper

A contract-oriented, Pythonic language for the Ethereum Virtual Machine (EVM), prioritizing security and simplicity.

- **Compiles to**: EVM bytecode
- **Tooling**: `vyper`, `eth-brownie`, `web3.py`
- **Example**:
  ```python
  counter: public(uint256)

  @external
  def __init__():
      self.counter = 0

  @external
  def increment():
      self.counter += 1
  ```

### PyTeal

A Python library for generating TEAL (Transaction Execution Approval Language) for Algorand smart contracts.

- **Compiles to**: TEAL assembly (then compiled to Algorand bytecode)
- **Tooling**: `pyteal`, `algosdk`, `goal`, `beaker`
- **Example**:
  ```python
  from pyteal import *

  program = And(
      Txn.type_enum() == TxnType.Payment,
      Txn.amount() <= Int(1000000),
      Txn.receiver() == Addr("ALGO_ADDRESS_HERE")
  )

  print(compileTeal(program, Mode.Signature, version=6))
  ```

### SmartPy

A Pythonic framework for writing Tezos smart contracts. SmartPy code is compiled to Michelson.

- **Compiles to**: Michelson bytecode
- **Tooling**: `smartpy-cli`, Tezos client
- **Example**:
  ```python
  import smartpy as sp

  class Counter(sp.Contract):
      def __init__(self, initial_value):
          self.data.value = initial_value

      @sp.entrypoint
      def add(self, delta):
          self.data.value += delta
  ```

### Xian

A native Python Layer-1 blockchain. Smart contracts are written in real Python, executed deterministically by all nodes using a sandboxed Python VM.

- **Executes**: Native Python in a restricted VM
- **Tooling**: `xian-contracting` (for local testing), deployment via **Chrome extension IDE**
- **Example**:
  ```python
  counter = Variable()

  @construct
  def init():
      counter.set(0)

  @export
  def increment():
      counter.set(counter.get() + 1)
      return counter.get()
  ```

## Getting Started

Install the core tools:

```bash
pip install vyper pyteal smartpy-cli xian-contracting
```

> **Note**: `xian-contracting` is for local testing. Deployment is done through the official Xian Chrome extension wallet and its built-in IDE.

## License

Released under the MIT License.
