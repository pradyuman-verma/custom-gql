# BlockFlow Studio

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://www.npmjs.com/package/@blockflow-labs/cli/v/1.0.7-beta.1?activeTab=readme)

Blockflow is a state-of-the-art data infrastructure platform that simplifies how you access and utilize on-chain data. With Blockflow, you can effortlessly transform, stream, and integrate data to meet your specific needs, whether you require real-time or historical data.

Blockflow's powerful command-line interface (CLI) allows you to harness the full potential of the platform, enabling you to focus on developing groundbreaking features for your Web3 application while we handle the complexities of the backend.

## Installation

Blockflow requires [Node.js](https://nodejs.org/) v18+ to run with typescript enabled.

```sh
npm i -g @blockflow-labs/cli
```

To verify that the CLI extension has been installed correctly

```sh
blockflow --version
```

Configure your cli with blockflow credentials to get started. Check [this](https://docs.blockflow.network/v/cli/getting-started/installation#accessing-access-key-and-secret-key-in-blockflow).

```sh
blockflow configure
```

## Project Initialization

To initialize a project in an empty directory, use the `blockflow init` command. This will open a command prompt where you can configure your project interactively.

```sh
blockflow init
```

## Configuration

BlockFlow Studio uses a YAML configuration file to manage your project settings. The configuration file should be named `studio.yaml` and located in the root folder of your project. Here are the configuration options:

| Configuration | Description                                                                                                                                          |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| `name`        | This is the name of your project.                                                                                                                    |
| `description` | A brief description of what your project does.                                                                                                       |
| `startBlock`  | The block number from which you want to start indexing. You can specify a specific block number or use `latest` to start from the most recent block. |
| `userId`      | Unique identifiers for your Blockflow user account.                                                                                                  |
| `projectId`   | Unique identifiers for your Blockflow project.                                                                                                       |
| `network`     | The blockchain network you’re working with.                                                                                                          |
| `user`        | The Blockflow username associated with your account.                                                                                                 |
| `schema`      | It contains a file path to your database schemas.                                                                                                    |
| `execution`   | It tells our system how to run the indexing process over the specified block range. You can choose between “parallel” or “sequential” execution.     |
| `resources`   | This section defines the smart contracts you want to index.                                                                                          |

### Resources

Within the resources section, you can define one or more data sources, each representing a specific blockchain network or smart contract. For each data source, you can provide the following details:

| Resources  | Description                                                                                                              |
| ---------- | ------------------------------------------------------------------------------------------------------------------------ |
| `Name`     | The name of the source data.                                                                                             |
| `Abi`      | The path to the smart contract's ABI file. The ABI defines the contract’s interface and is used to interact with it.     |
| `Type`     | The type of resource.                                                                                                    |
| `Address`  | The address of the source data.                                                                                          |
| `Triggers` | It contains an array of configurations linking smart contract events/functions to their corresponding handler functions. |

To read more about `studio.yaml` configuration. Check this [doc](https://docs.blockflow.network/v/cli/deep-dive/configuring-yaml).

### Blockflow Commands

To generate an events/functions list in `studio.yaml`, which will be used to configure the handler, use the `blockflow generate` command. This will automatically fetch the added contracts ABIs and update the events/functions list.

```sh
blockflow generate
```

To generate handlers in` studio.yaml`, use the `blockflow codegen` command. The handler will be generated at the `Resources?.Trigger?.Handler` path.

```sh
blockflow codegen
```

#### Instance Testing

To test the code and generate a local mongo database, use the `blockflow instance-test` command. This will produce a database named blockflow_studio with collection name BLOCKFLOW_STUDIO.

```bash
blockflow instance-test
```

> you can even provide a start block `--startBlock <startBlock>`, or range of blocks to test `--range 10`

#### Deploy Instance

Once the project is created and tested, you can deploy it using the `blockflow instance-deploy` command. This will deploy the handler to the blockflow server for syncing.

```bash
blockflow instance-deploy
```

#### API Testing

You can create Rest API endpoints to access data filled in your database through Blockflow instances. To test API you need to ensure your local MongoDB is running and filled with instance data.

```bash
blockflow api-test
```

#### Deploy API

To deploy the API, use the `blockflow api-deploy` command.

```bash
blockflow api-deploy
```

For more detailed information about BlockFlow Studio and its features, please refer to our comprehensive [documentation](https://docs.blockflow.network/v/cli).

> Want to contribute or see interesting example?
> Great! Star mark this examples [repo](https://github.com/BlockFloww/cli-examples).
