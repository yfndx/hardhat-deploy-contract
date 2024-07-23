

# Swisstronik Tesnet Technical Task 1

Link: [Click!](https://www.swisstronik.com/testnet2/dashboard)

## Hardhat Deploy Contract

This repository contains a Hardhat project for deploying Ethereum smart contracts. Below is an explanation of the key components and how to deploy the contract.

## Explanation of Code

### Solidity Contract: `contracts/MyContract.sol`

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyContract {
    string public message;

    constructor(string memory _message) {
        message = _message;
    }

    function setMessage(string memory _message) public {
        message = _message;
    }
}
```

- **`message`**: A public state variable to store a string.
- **`constructor`**: Initializes the contract with a message.
- **`setMessage`**: Updates the message.

### Deployment Script: `scripts/deploy.js`

```javascript
async function main() {
    const [deployer] = await ethers.getSigners();
    console.log("Deploying contracts with the account:", deployer.address);

    const MyContract = await ethers.getContractFactory("MyContract");
    const myContract = await MyContract.deploy("Hello, Hardhat!");
    console.log("MyContract deployed to:", myContract.address);
}

main()
    .then(() => process.exit(0))
    .catch((error) => {
        console.error(error);
        process.exit(1);
    });
```

- **`main` function**: Deploys the `MyContract` with an initial message "Hello, Hardhat!".
- **`ethers.getSigners`**: Retrieves the deployer's account.
- **`ethers.getContractFactory`**: Prepares the contract for deployment.
- **`MyContract.deploy`**: Deploys the contract to the specified network.

## Deploying the Contract

### Prerequisites

Ensure you have the following installed:

- [Node.js](https://nodejs.org/)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)

### Steps

1. **Install dependencies**:
    ```bash
    npm install
    # or
    yarn install
    ```

2. **Compile the contract**:
    ```bash
    npx hardhat compile
    ```

3. **Deploy the contract**:
    ```bash
    npx hardhat run scripts/deploy.js --network <network-name>
    ```
    Replace `<network-name>` with the desired network, such as `localhost`, `ropsten`, or `mainnet`.

### Example Configuration in `hardhat.config.js`

```javascript
require("@nomiclabs/hardhat-waffle");

module.exports = {
    solidity: "0.8.4",
    networks: {
        localhost: {
            url: "http://127.0.0.1:8545"
        },
        ropsten: {
            url: `https://ropsten.infura.io/v3/YOUR_INFURA_PROJECT_ID`,
            accounts: [`0x${YOUR_PRIVATE_KEY}`]
        }
    }
};
```

Replace `YOUR_INFURA_PROJECT_ID` with your Infura project ID and `YOUR_PRIVATE_KEY` with your Ethereum account private key.

## License

This project is licensed under the MIT License.

