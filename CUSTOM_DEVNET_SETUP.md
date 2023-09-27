## 📝 Custom Devnet setup

It is possible to test PEPC-Boost on a custom devnet using kurtosis. This is useful for testing PEPC-Boost on a custom devnet with a specific configuration. This guide will walk you through the steps to setup a custom devnet and test PEPC-Boost on it.

### 📝 Prerequisites

You can learn how to setup a kurtosis devnet using their detailed docs at https://github.com/kurtosis-tech/ethereum-package

### 📝 Setup

To run a setup with the PEPC-Boost relay and PEPC-Boost builder, you need to run the following commands:

```bash
kurtosis run --enclave my-testnet github.com/kurtosis-tech/eth2-package  "$(cat ./network.json)";
```

The network.json file contents can be found below

```json
{
  "participants": [
    {
      "el_client_type": "geth",
      "el_client_image": "ethereum/client-go:latest",
      "el_client_log_level": "",
      "el_extra_params": [],
      "cl_client_type": "lighthouse",
      "cl_client_image": "",
      "cl_client_log_level": "",
      "beacon_extra_params": [],
      "validator_extra_params": [],
      "builder_network_params": null,
      "count": 1
    }
  ],
  "network_params": {
    "seconds_per_slot": 12,
    "slots_per_epoch": 32,
    "capella_fork_epoch": 1
  },
  "mev_type": "full",
  "mev_params": {
    "mev_relay_image": "<pepc-boost-relay-image>",
    "mev_builder_image": "<pepc-boost-builder-image>",
    "mev_flood_seconds_per_bundle": 7,
    "launch_custom_flood": true
  }
}
```

You can use `public.ecr.aws/t1d5h1w5/pepc-boost-relay:latest` as the latest pepc-boost-relay image and `public.ecr.aws/t1d5h1w5/pepc-boost-builder:latest` as the latest pepc-boost-builder image with it which contains the `assembleBlock` RPC.
Note that these images are bleeding edge and might contain breaking changes.

### 📝 Testing

To submit ToB txs, you can follow the guide provided in the README of the following repo:

https://github.com/bharath-123/pepc-boost-testing/tree/devnet-testing

The code should be pretty readable and it should be easy to submit a ToB tx with this api.

Post submission of a ToB tx using the above repo, you can monitor the pepc-boost-relay website which you can connect to by connecting to the port of the pepc-boost-relay website.

Monitor the recently delivered payloads for the slot for which you have submitted your ToB tx. If your validator payout is fairly high, you will see a delivered payload with fairly high value.

You can pick the block hash of the block from the website and run the block inspection code available in above repo. With this you can examine the txs and check if your ToB txs are on the top.


