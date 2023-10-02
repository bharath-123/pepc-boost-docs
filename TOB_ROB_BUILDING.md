## 📝 ToB RoB Building

When the builder submits a block to the PEPC-Boost relayer, the relayer checks the existing ToB tx cache for the particular slot and parent hash. If it finds the ToB txs and the sum of the ToB tx value and RoB tx value is the highest seen so far. We then call the Block Assembler RPC API, sending the ToB txs, and the Builder block submit request as parameters. The block assembler assembles the block with the ToB txs at the top and the RoB txs in the rest of the block. If successful, it returns the final execution payload to the relayer which it stores as the final block.
The Block Assembler is an actor in the PEPC-Boost design, responsible for merging searcher ToB txs and RoB blocks built by builders. It is implemented as an RPC similar to `ValidateBlockSubmission`
In cases, where a block is submitted but there are no ToB txs for the particular slot, we just simulate the block like the status quo of MEV relayers.

![Relayer Block building](https://raw.githubusercontent.com/bharath-123/pepc-boost-docs/main/diagrams/TobRobBlockBuilding.png)

### Relevant PRs

[[PEPC-Boost][5] Add types to integrate with the block assembler](https://github.com/bharath-123/pepc-boost-relay/pull/8)

[[PEPC-Boost][6] Block Assembler Client](https://github.com/bharath-123/pepc-boost-relay/pull/9)

[[PEPC-Boost][7] Call block assembler with ToB txs whenever blocks are submitted](https://github.com/bharath-123/pepc-boost-relay/pull/10)

[[PEPC-Boost][8] Block Assembler Client Integration tests](https://github.com/bharath-123/pepc-boost-relay/pull/11)