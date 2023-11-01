## 📝 ToB RoB Building

When the builder submits a block to the PEPC-Boost relayer, the relayer checks the existing ToB tx cache for the particular slot and parent hash. If it finds the ToB txs and the sum of the ToB tx value and RoB block value is the highest seen so far. We then call the Block Assembler RPC API, sending the ToB txs, and the RoB block as parameters. The block assembler assembles the block with the ToB txs at the top and the RoB txs in the rest of the block. If successful, it returns the final execution payload containing the ToB and RoB txs to the relayer which it stores in the final block.
More info on the Block assembler can be found in `BLOCK_ASSEMBLY.md`
In cases, where a block is submitted but there are no ToB txs for the particular slot, we just simulate the block like the status quo of MEV relayers.
We also cache the highest value RoB block for a particular slot and parent hash. This is useful to re-build the highest value RoB with ToB bundles that are subsequently submitted for the same slot and parent hash. To trigger the re-build of the current highest ToB bundle with the current highest RoB bundle, 
we need to trigger the `/relay/v1/builder/rob_blocks` endpoint with query params `slot` and `parent_hash` set to the slot and parent hash at which the ToB bundle was submitted.

![Relayer Block building](https://raw.githubusercontent.com/bharath-123/pepc-boost-docs/main/diagrams/TobRobBlockBuilding.png)

### Relevant PRs

[[PEPC-Boost][5] Add types to integrate with the block assembler](https://github.com/bharath-123/pepc-boost-relay/pull/8)

[[PEPC-Boost][6] Block Assembler Client](https://github.com/bharath-123/pepc-boost-relay/pull/9)

[[PEPC-Boost][7] Call block assembler with ToB txs whenever blocks are submitted](https://github.com/bharath-123/pepc-boost-relay/pull/10)

[[PEPC-Boost][8] Block Assembler Client Integration tests](https://github.com/bharath-123/pepc-boost-relay/pull/11)