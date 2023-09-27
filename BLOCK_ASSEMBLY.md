## 📝 Block Assembly Architecture

The PR describes the changes done in the PEPC Boost builder.

The changes are mainly on implementing a block assembler. The Block Assembler is an actor in the PEPC-Boost design, responsible for merging searcher ToB txs and RoB blocks built by builders. It is implemented as an RPC similar to `ValidateBlockSubmission`

The Block Assembler RPC is called by the PEPC-Boost relay. When the builder submits a block to the PEPC-Boost relayer, the relayer checks the existing ToB tx cache for the particular slot and parent hash. If it finds the ToB txs and the sum of the ToB tx value and RoB tx value is the highest seen so far. We then call the Block Assembler RPC API, sending the ToB txs, and the Builder block submit request as parameters. The block assembler assembles the block with the ToB txs at the top and the RoB txs in the rest of the block. If successful, it returns the final execution payload to the relayer which it stores as the final block.

Below is a diagram which shows the architecture:
![Block Assembler](https://raw.githubusercontent.com/bharath-123/pepc-boost-docs/main/diagrams/BlockAssembler.png)


The PRs for the implementation:
[[PEPC-Boost][1] add types for block assembler rpc + minor refactor](https://github.com/bharath-123/pepc-boost-builder/pull/7)
[[PEPC-Boost][2] Block Assembler Implementation](https://github.com/bharath-123/pepc-boost-builder/pull/9)
[[PEPC-Boost][3] Block Assembler Tests](https://github.com/bharath-123/pepc-boost-builder/pull/11)

