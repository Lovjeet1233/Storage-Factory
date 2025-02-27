# SimpleStorage Project

## Overview

This repository contains a set of Solidity smart contracts that demonstrate fundamental concepts in Ethereum smart contract development, focusing on storage patterns and factory design patterns.


## Contracts

The project consists of the following smart contracts:

### SimpleStorage.sol

A basic storage contract that allows for:
- Storing and retrieving a favorite number
- Adding persons with their names and favorite numbers
- Mapping from names to favorite numbers

```solidity
contract SimpleStorage {
    uint256 myFavoriteNumber;
    
    struct Person {
        uint256 favoriteNumber;
        string name;
    }
    
    Person[] public listOfPeople;
    mapping(string => uint256) public nameToFavoriteNumber;
    
    // Store a favorite number
    function store(uint256 _favoriteNumber) public virtual {
        myFavoriteNumber = _favoriteNumber;
    }
    
    // Retrieve the stored favorite number
    function retrieve() public view returns (uint256) {
        return myFavoriteNumber;
    }
    
    // Add a person with their name and favorite number
    function addPerson(string memory _name, uint256 _favoriteNumber) public {
        listOfPeople.push(Person(_favoriteNumber, _name));
        nameToFavoriteNumber[_name] = _favoriteNumber;
    }
}
```

### StorageFactory.sol

A factory contract that can:
- Create new instances of SimpleStorage contracts
- Store values in any created SimpleStorage contract
- Retrieve values from any created SimpleStorage contract

```solidity
contract StorageFactory {
    SimpleStorage[] public listOfSimpleStorageContracts;
    
    // Create a new SimpleStorage contract
    function createSimpleStorageContract() public {
        SimpleStorage simpleStorageContractVariable = new SimpleStorage();
        listOfSimpleStorageContracts.push(simpleStorageContractVariable);
    }
    
    // Store a number in a specific SimpleStorage contract
    function sfStore(uint256 _simpleStorageIndex, uint256 _simpleStorageNumber) public {
        listOfSimpleStorageContracts[_simpleStorageIndex].store(_simpleStorageNumber);
    }
    
    // Get a number from a specific SimpleStorage contract
    function sfGet(uint256 _simpleStorageIndex) public view returns (uint256) {
        return listOfSimpleStorageContracts[_simpleStorageIndex].retrieve();
    }
}
```

## Features

- **Basic Storage**: Store and retrieve numerical values
- **Struct Implementation**: Store structured data using Solidity structs
- **Arrays**: Use dynamic arrays to store collections of structured data
- **Mappings**: Implement key-value storage with Solidity mappings
- **Factory Pattern**: Create and manage multiple contract instances
- **Contract Interaction**: Interact with deployed contracts from another contract

## Requirements

- Solidity ^0.8.0
- Ethereum development environment (Hardhat, Truffle, or Foundry)
- Web3 provider (Infura, Alchemy, or local node)

## Usage

### Deployment

1. Deploy `SimpleStorage.sol`
2. Deploy `StorageFactory.sol` with the address of the deployed SimpleStorage contract

### Interacting with SimpleStorage

```javascript
// Store a favorite number
await simpleStorage.store(42);

// Retrieve the stored number
const favoriteNumber = await simpleStorage.retrieve();

// Add a person
await simpleStorage.addPerson("Alice", 7);

// Get a person's favorite number
const alicesFavoriteNumber = await simpleStorage.nameToFavoriteNumber("Alice");
```

### Interacting with StorageFactory

```javascript
// Create a new SimpleStorage contract
await storageFactory.createSimpleStorageContract();

// Store a value in the first SimpleStorage contract
await storageFactory.sfStore(0, 42);

// Retrieve the value from the first SimpleStorage contract
const value = await storageFactory.sfGet(0);
```

## License

This project is licensed under the MIT License - see the license statement at the top of each file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgements

- Solidity documentation
- Ethereum community
