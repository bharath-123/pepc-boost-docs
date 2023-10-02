## 📝 Per Slot ToB Auction Architecture in PEPC-Boost

One of the pivotal elements within the PEPC-Boost ecosystem is the per slot ToB (Top of Block) auction.

Within this auction, searchers have the opportunity to participate by submitting transactions (txs) they wish to see included at the top of the block proposed for that specific slot. Importantly, these transactions are built solely on top of their chosen parent hash. The role of the relayer in this process is to retain the highest-value transactions submitted by searchers at any given time. The value of these transactions is determined by the payout offered by the searcher. Note that searchers can only submit txs they want to include in the current slot or the next slot.  

To minimize conflicts with the RoB (Rest of Block), the ToB transactions undergo state interference checks. Specifically, they are screened to identify whether they involve an ETH/USDC swap for the initial versions. Subsequently, these ToB transactions are stored in a Redis cache, where the slot and parent hash serve as the keys. Notably, the ToB transactions have a cache Time-To-Live (TTL) of 45 seconds.

Searchers submit their bids for ToB transactions through the /relay/v1/builder/tob_txs API endpoint. 

![TOB bid auction](https://raw.githubusercontent.com/bharath-123/pepc-boost-docs/main/diagrams/TOBAuctionFlow.png)


### Relevant PRs

[[PEPC-Boost][1] ToB bid auction types](https://github.com/bharath-123/pepc-boost-relay/pull/4)

[[PEPC-Boost][2] Redis datastore implementation for ToB bid auction](https://github.com/bharath-123/pepc-boost-relay/pull/5)

[[PEPC-Boost][3] ToB bid auction implementation](https://github.com/bharath-123/pepc-boost-relay/pull/6)

[[PEPC-Boost][4] Add tests for the ToB bid tx auction impl](https://github.com/bharath-123/pepc-boost-relay/pull/7)