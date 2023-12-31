## 📝 ToB Auction

PEPC-Boost allows searchers to bid for the top of the block (ToB) of the block proposed for the particular slot.

Within this auction, searchers have the opportunity to participate by submitting transactions (txs) they wish to see included at the top of the block proposed for that specific slot. The searchers also have to specify the parent hash of the block on top which they built their ToB txs. The PEPC-Boost relay stores the highest value ToB txs sent for a given slot and parent hash. The value of the ToB transactions is determined by the payout offered by the searcher to the proposer of the block. Note that searchers can only submit txs they want to include in the current slot or the next slot.  

We currently only allow CEX-DEX arbitrage related txs on the ToB. In the V0 of PEPC-Boost, we only allow 1 ToB tx along with the payout which is a uniswap v3 ETH/USDC swap. In future versions, we plan to expand the slots available for auction in the ToB. This will enable a searcher to bid for more space on the ToB. This auction essentially opens up the blockspace of validators not only the builders but also the searchers.

Searchers submit the ToB txs along with a payout tx to the proposer of the block for the provided slot. They also provide the parent hash on top of which they have built their ToB tx. They submit to the `/relay/v1/builder/tob_txs` endpoint. You can refer to the diagram for the workflow of this endpoint.

![TOB bid auction](https://raw.githubusercontent.com/bharath-123/pepc-boost-docs/main/diagrams/TOBAuctionFlow.png)


### Relevant PRs

[[PEPC-Boost][1] ToB bid auction types](https://github.com/bharath-123/pepc-boost-relay/pull/4)

[[PEPC-Boost][2] Redis datastore implementation for ToB bid auction](https://github.com/bharath-123/pepc-boost-relay/pull/5)

[[PEPC-Boost][3] ToB bid auction implementation](https://github.com/bharath-123/pepc-boost-relay/pull/6)

[[PEPC-Boost][4] Add tests for the ToB bid tx auction impl](https://github.com/bharath-123/pepc-boost-relay/pull/7)