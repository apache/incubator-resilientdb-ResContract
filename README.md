```
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#  http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
```
**DEPRECATION NOTICE**

This repository is deprecated.
Active development now continues in the [ResilientDB Monorepo](https://github.com/apache/incubator-resilientdb).

The ResContract CLI can be found at [ecosystem/smart-contract/rescontract](https://github.com/apache/incubator-resilientdb/tree/master/ecosystem/smart-contract/rescontract).

# ResContract CLI 🚀

The **ResContract CLI** is a command-line tool for creating, deploying, and managing smart contracts within the ResilientDB ecosystem. It provides a streamlined interface for developers and students to interact with smart contracts efficiently.

## Table of Contents

- [Features ✨](#features-)
- [Prerequisites](#prerequisites)
- [Installation 🛠️](#installation-️)
- [Usage](#usage)
  - [Commands](#commands)
    - [create Command](#create-command)
    - [compile Command](#compile-command)
    - [deploy Command](#deploy-command)
    - [add_address Command](#add_address-command)
    - [list-deployments Command](#list-deployments-command)
    - [clear-registry Command](#clear-registry-command)
- [Configuration ⚙️](#configuration-️)
  - [Setting the ResDB_Home Variable](#setting-the-resdb_home-variable)
    - [Option 1: Set `ResDB_Home` Environment Variable](#option-1-set-resdb_home-environment-variable)
    - [Option 2: Use a `config.yaml` File](#option-2-use-a-configyaml-file)
- [Contributing](#contributing)
- [License](#license)

## Features ✨

- **Create Smart Contracts**: Generate new smart contract templates.
- **Compile Contracts**: Compile Solidity contracts to JSON.
- **Deploy Smart Contracts**: Deploy contracts to the blockchain with automatic registry tracking.
- **Address Management**: Add external addresses to the system.
- **Deployment Registry**: Track and manage deployed contracts with built-in registry commands.

## Prerequisites

Before installing and using the ResContract CLI, ensure you have the following prerequisites installed on your system:

- **Node.js (version >= 14)**: [Download and install Node.js](https://nodejs.org/en/download/)
- **npm**: Comes with Node.js. Ensure it's up-to-date.
- **Solidity Compiler (`solc`)**: Required to compile smart contracts.

### Installing `solc`

#### Linux (Ubuntu/Debian)

```bash
sudo add-apt-repository ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install -y solc
```

#### macOS
```bash
brew update
brew upgrade
brew tap ethereum/ethereum
brew install solidity
```

## Installation 🛠️

Install the ResContract CLI globally using npm:

```bash
npm install -g rescontract-cli
```` 

## Configuration ⚙️

### Setting the ResDB_Home Variable

Before using the ResContract CLI, you  **must**  set the  `ResDB_Home`  environment variable or provide the path to your ResilientDB installation in a  `config.yaml`  file. The CLI will  **not**  prompt you for this path and will exit with an error if it's not set.

#### Option 1: Set  `ResDB_Home`  Environment Variable

Set the  `ResDB_Home`  environment variable to point to the directory where ResilientDB is installed.

**Linux/macOS:**
```bash
export ResDB_Home=/path/to/resilientdb
```

Add the above line to your  `.bashrc`  or  `.zshrc`  file to make it persistent.

#### Option 2: Use a  `config.yaml`  File

Update the `config.yaml`  file in the same directory where you run the  `rescontract`  command or in your home directory.

**Example  `config.yaml`:**
```yaml
ResDB_Home: /path/to/resilientdb
```

Ensure the  `ResDB_Home`  path is correct.

> **Note:**  The CLI checks for  `config.yaml`  in the current directory first, then in your home directory.

## Usage

After installation, you can use the  `rescontract`  command in your terminal.

```bash
rescontract <command> [options]
```

### Commands

#### create Command

Initializes a new account using ResilientDB's smart contract tools.

**Usage:**
```bash
rescontract create --config <path_to_config>
```
-   `--config, -c`: Path to the configuration file.

**Example:**

```bash
rescontract create --config ~/resilientdb/config/service.config
```

#### compile Command

Compiles a Solidity smart contract into a JSON file using  `solc`.

**Usage:**
```bash
rescontract compile --sol <inputFile.sol> --output <outputFile.json>
```

-   `--sol, -s`: Path to the Solidity smart contract file.
-   `--output, -o`: Name of the resulting JSON file.

**Example:**

```bash
rescontract compile --sol contracts/MyToken.sol --output build/MyToken.json
```

#### deploy Command

Deploys the smart contract to the blockchain.

**Usage:**

```bash
rescontract deploy --config <service.config> --contract <contract.json> \
--name <tokenName> --arguments "<parameters>" --owner <address>
```

-   `--config, -c`: Client configuration path.
-   `--contract, -p`: Path to the contract JSON file.
-   `--name, -n`: Name of the contract.
-   `--arguments, -a`: Parameters to create the contract object (enclosed in quotes).
-   `--owner, -m`: Contract owner's address.

**Example:**

```bash
rescontract deploy --config ~/resilientdb/config/service.config \
--contract build/MyToken.json --name MyToken \
--arguments "1000000" --owner 0xYourAddress
```

#### add_address Command

Adds an external address to the system for contract interactions.

**Usage:**
```bash
rescontract add_address --config <path> --external-address <address>
```

-   `--config, -c`: Path to the configuration file.
-   `--external-address, -e`: External address to add to the system.

**Example:**
```bash
rescontract add_address --config ~/resilientdb/config/service.config \
--external-address 0xExternalAddress
```

#### list-deployments Command

Lists all deployed contracts tracked in the registry.

**Usage:**
```bash
rescontract list-deployments
```

**Example:**
```bash
rescontract list-deployments
```

This command displays all deployed contracts with their owner addresses, contract names, and contract addresses.

#### clear-registry Command

Clears the deployed contracts registry.

**Usage:**
```bash
rescontract clear-registry
```

**Example:**
```bash
rescontract clear-registry
```

**Warning:** This command permanently removes all deployment tracking information.

## Deployment Registry 📋

The ResContract CLI automatically tracks all deployed contracts in a registry file located at `~/.rescontract_deployed_contracts.json`. This registry provides several benefits:

- **Duplicate Prevention**: Prevents deploying the same contract with the same owner and name
- **Contract Tracking**: Maintains a record of all deployed contracts with their addresses
- **Easy Management**: Use `list-deployments` to view all contracts and `clear-registry` to reset

The registry stores the following information for each deployment:
- Owner address
- Contract name
- Contract address
- Deployment timestamp

## License

This project is licensed under the MIT License - see the  [LICENSE](LICENSE)  file for details.
