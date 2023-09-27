## ToB and RoB block building

Whenever a builder builds an RoB block, it checks the ToB tx cache for the highest value ToB txs for the particular slot and parent hash. If the sum of the value of the ToB tx and RoB block is higher than the given block, we send it to the block assembler to assemble a final payload with the ToB txs on the top and the RoB txs in the rest of the block. This final payload is stored with the final builder bid in the payload database.
The Block Assembler assembles the ToB searcher txs with the block produced by the builder. The Block Assembler is implemented as an RPC call in the builder, similar to `ValidateBlockSubmissionV2` RPC calls.
If there are no ToB txs for the particular slot and parent hash, the relay simulates the block using the `ValidateBlockSubmissionV2` RPC call.

![Relayer Block building](https://raw.githubusercontent.com/bharath-123/pepc-boost-docs/main/diagrams/TobRobBlockBuilding.png)

