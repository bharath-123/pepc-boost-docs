## 📝 State Interference Checks

In PEPC-Boost, we check the ToB txs for whether they are a specific type of tx, like an Eth/Usdc swap. To check if a tx is an Eth/Usdc swap, for EOA's we can check the data field and parse it for the specific type of method on uniswap. But if the swap is part of a smart contract call, we cannot infer whether an Eth/Usdc swap is happening from the data field in the tx.
To achieve this, we use the call tracing feature available in the execution layer. We use the `debug_traceCall` RPC call and pass in the tx details. We receive detailed call traces from the execution layer with this RPC call. The traces contain info on each smart contract call made by the root call. We then use `abigen` to generate go-bindings for some common smart contracts. We use these bindings to get the smart contract method ids for the particular txs we want to check.
State interference checks change based on the n/w we run in. 
