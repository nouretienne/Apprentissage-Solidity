## The Ethereum Virtual Machine

### Overview

The Ethereum Virtual Machine or EVM is the runtime environment for smart contracts in Ethereum. It is not only sandboxed but actually completely isolated, which means that code running inside the EVM has no access to network, filesystem or other processes. Smart contracts even have limited access to other smart contracts.

### Accounts

There are two kinds of accounts in Ethereum which share the same address space: Externally-owned accounts that are controlled by public-private key pairs (i.e. humans) and contract acounts which are controlled by the code stored together with the account.

The address of an externally-owned account is determined from the public key while the address of a contract is determined at the time the contract is created (it is derived from the creator address and the number of transactions sent from that address, the so-called "nonce")

Regardless of whether or not the account sotres code, the two types are treated equaly by the EVM.

Furthermore, every account has a balance in Ether (in "Wei" to be exact, ```1 ether``` is ```10**18 wei```) which can be modified by sending transactions that include Ether.

### Transactions

A transaction is a message that is sent from one account to another account (which might be the same or empty, see below). It can include binary data (which is called "payload") and Ether.

If the target account contains code, that code is executed and the payload is provided as input data. 

If the target account is not set (the transaction does not have a recipient or the recipient is set to ```null```), the transaction creates a **new contract**. As already mentioned, the address of that contract is not the zero address but an address derived from the sender and its number of transaction sent (the "nonce"). The payload of such a contract creation transaction is taken to be EVM bytecode and executed. The output data of this execution is permanently stored as the code of the contract. This means that in order to create a contract, you do not send the actual code of the contract, but in fact code that returns that code when executed.

Note:

While a contract is being created, its code is still empty. Because of that, you should not call back into the contract under construction until its constructor has finished executing.

### Gas

Upon creation, each transaction is charged with a certain amount of **gas** that has to be paid for by the organisator of the transactionl (```tx.origin```). While the EVM executes the transaction, the gaz is gradually depleted according to specific rules. If the gas is used up at any point (i.e. it would be negative), an out-of-gas exception is triggered, which ends execution and reverts all modifications made to the state in the current call frame.

This mechanism incentivizes economical use of EVM execution time and also compensates EVM executors (i.e. miners / stakers) for their work. Since each block has a maximum amount of gas, it also limits the amount of work needed to validate a block.

The **gas price** is a value set by the originator of the transaction, who has to pay ```gas_price``` up front to the EVM executor. If some gas is left after execution, it is refunded to the transaction originator. In case of an exception that reverts changes, already used up gas is not refunded.

Since EVM executors can choose to include a transaction or not, transaction senders cannot abuse the system by setting a low gas price.
