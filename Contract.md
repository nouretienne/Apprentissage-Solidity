Structure of a contract

Contracts are similar to classes in object-oriented languages. Each contract can contain declarations of State Variables, Functions, Functiosn Modifiers, Errors, Events, Struct Type and Enum Type. 
Furthermore contracts can inherit from other contracts.

There are also special kinds of contracts called libraries and interfaces.

State variables
State variables are variables whose values are either permanently stored in contract storage or, alternatively temporarly stored in transient storage which is cleaned at the end of each transaction. 

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.4.0 <0.9.0;

contract SimpleStorage {
    uint storedData; // State variable
    // ...
}
```

