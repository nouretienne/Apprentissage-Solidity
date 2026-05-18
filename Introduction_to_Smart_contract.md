## Introduction to Smart Contract

### A simple Smart Contract

Let us begin with a basic example that sets the value of a variable and exposes it for other contracts to access.

Storage Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.4.16 <0.9.0;

contract SimpleStorage {
    uint256 storedData;

    function set(uint256 x) public {
        storedData = x;
    }

    function get() public view returns (uint) {
        return storedData;
    }
}
``` 
```solidity
//SPDX-License-Identifier: MIT
pragma >=0.4.0 < 0.9.0;

contract SimpleStorage {
    uint256 storedData;

    function set(uint256 x) public {
        storedData = x;
    }

    function get() public view returns (uint) {
        return storedData;
    }
    }
```