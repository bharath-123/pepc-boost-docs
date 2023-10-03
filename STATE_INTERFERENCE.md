## 📝 State Interference Checks

In PEPC-Boost, we check the ToB txs for whether they are a specific type of tx, like an Eth/Usdc swap. To check if a tx is an Eth/Usdc swap, for EOA's we can check the data field and parse it for the specific type of method on uniswap. But if the swap is part of a smart contract call, we cannot infer whether an Eth/Usdc swap is happening from the data field in the tx.
To achieve this, we use the call tracing feature available in the execution layer(https://geth.ethereum.org/docs/developers/evm-tracing). We use the `debug_traceCall` RPC call and pass in the tx details. We receive detailed call traces from the execution layer with this RPC call. The traces contain info on each smart contract call made by the root call. We check each trace to check whether a trace matches an ETH/USDC swap on uniswap v3.
To make this check, we need to check the input data of the call for the method id of the smart contract call and the parameters passed to the smart contract call.
To perform the input data checks in a robust fashion, we make use of `abigen` to generate go-bindings for the uniswap v3 smart contracts. We use these bindings to get the smart contract method ids and out of the box methods to unpack a call's input data into the parameters passed to the smart contract call.
State interference checks change based on the n/w we run in. 

### Relevant PRs

[[PEPC-Boost][9] Tx tracing infra types](https://github.com/bharath-123/pepc-boost-relay/pull/13)

[[PEPC-Boost][10] Implement tracing infra](https://github.com/bharath-123/pepc-boost-relay/pull/14)

[[PEPC-Boost][11] Implement custom devnet state interference checks](https://github.com/bharath-123/pepc-boost-relay/pull/15)

[[PEPC-Boost][12] Custom devnet state interference checks tests](https://github.com/bharath-123/pepc-boost-relay/pull/16)

[[PEPC-Boost][13] Add state interference checks for Goerli](https://github.com/bharath-123/pepc-boost-relay/pull/17)

[[PEPC-Boost][14] Goerli state interference checks](https://github.com/bharath-123/pepc-boost-relay/pull/18)