## 📝 Block Assembly Architecture

The PR describes the changes done in the PEPC Boost builder.

The changes are mainly on implementing a block assembler. The Block Assembler is an actor in the PEPC-Boost design, responsible for merging searcher ToB txs and RoB blocks built by builders and returning an execution payload which includes the ToB txs at the top of the block and the RoB txs occupying the remaining of the block. It is implemented as an RPC similar to `ValidateBlockSubmissionV2`

The Block Assembler RPC is called by the PEPC-Boost relay which passes the ToB txs and RoB txs to be merged and built into a final block.

Below is a diagram which shows the architecture:
![Block Assembler](https://raw.githubusercontent.com/bharath-123/pepc-boost-docs/main/diagrams/BlockAssembler.png)


The PRs for the implementation:

[[PEPC-Boost][1] add types for block assembler rpc + minor refactor](https://github.com/bharath-123/pepc-boost-builder/pull/7)

[[PEPC-Boost][2] Block Assembler Implementation](https://github.com/bharath-123/pepc-boost-builder/pull/9)

[[PEPC-Boost][3] Block Assembler Tests](https://github.com/bharath-123/pepc-boost-builder/pull/11)

