# PEPC-Boost Docs

This repo contains all documentation related to PEPC-Boost

`ARCHITECTURE.md` - Contains the overall architecture of PEPC-Boost

`BLOCK_ASSEMBLY.md` - Conatains the architecture of the block assembler

`CUSTOM_DEVNET_SETUP.md` - Contains the steps to setup a custom devnet and test PEPC-Boost on it

`TOB_ROB_BUILDING.md` - Contains the workflow in the relayer for how ToB and RoB blocks are selected and merged to get a final block

`TOB_AUCTION.md` - Contains the architecture of the auction for searchers to include their txs at the ToB


## Glossary

`PEPC` - Protocol Enforced Proposer Commitments

`ToB` - Top of the block

`RoB` - Rest of the block

`ToB value` - The value of the ToB txs which is determined by the payout offered by the searcher to the proposer of the block.

`ToB tx` - The transaction which the searcher wants to include at the top of the block

`Builder` - The entity which builds the RoB block

`Searcher` - The entity which bids for the ToB slot

