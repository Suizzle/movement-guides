# Configuring a Sui dApp for Movement Network

In this guide for Sui developers, we'll learn how easy it is to create a Sui dApp React frontend and configure your dApp for Movement Network's M2 blockchain.

## Create a new Sui dApp project with `@mysten/create-dapp` 

```
pnpm create @mysten/dapp
```

([Install pnpm](https://pnpm.io/installation) first if needed.)

When you're prompted `Which starter template would you like to use?`, select `react-e2e-counter`.

Then give your app a unique name or use the default name, `my-first-sui-dapp`.

Navigate into your dApp's folder:

```
cd <your dapp name>
```
Open the dApp codebase with your favorite editor:
```
code .
```
Install dependencies:
```
npm install
```
And run your dApp locally:
```
npm run dev
```
Your dApp will appear in your browser:

![Dapp Starter Template](./images/dapp-starter-template)

## Configure your Sui dApp for Movement Network (M2)
Begin by modifying `networkConfig.ts` where network information is defined: 

```  
const { networkConfig, useNetworkVariable, useNetworkVariables } =
  createNetworkConfig({
    devnet: {
      url: getFullnodeUrl("devnet"),
      variables: {
        counterPackageId: DEVNET_COUNTER_PACKAGE_ID,
      },
    },
    mainnet: {
      url: getFullnodeUrl("mainnet"),
      variables: {
        counterPackageId: MAINNET_COUNTER_PACKAGE_ID,
      },
    },
  });
```
Add Movement Network's `m2` using the RPC url `https://devnet.m2.movementlabs.xyz:443`:

```
const { networkConfig, useNetworkVariable, useNetworkVariables } =
  createNetworkConfig({
    devnet: {
      url: getFullnodeUrl("devnet"),
      variables: {
        counterPackageId: DEVNET_COUNTER_PACKAGE_ID,
      },
    },
    mainnet: {
      url: getFullnodeUrl("mainnet"),
      variables: {
        counterPackageId: MAINNET_COUNTER_PACKAGE_ID,
      },
    },
    m2: {
      url: "https://devnet.m2.movementlabs.xyz:443",
      variables: {
        counterPackageId: M2_COUNTER_PACKAGE_ID,
      },
    },
  });
```
At the top of the file, import `M2_COUNTER_PACKAGE_ID`:
```
import {
  DEVNET_COUNTER_PACKAGE_ID,
  MAINNET_COUNTER_PACKAGE_ID,
  M2_COUNTER_PACKAGE_ID
} from "./constants.ts";
```

You can see that no package IDs are pre-configured in `constants.ts`.

```
export const DEVNET_COUNTER_PACKAGE_ID = "0xTODO";
export const MAINNET_COUNTER_PACKAGE_ID = "0xTODO";
```
To publish your Move package to M2, navigate to the `counter` directory:

`cd move/counter`

Follow [this guide](https://docs.movementlabs.xyz/developers/sui-developers/using-sui-cli) to use Sui CLI.

Or [use `movement sui`](https://docs.movementlabs.xyz/developers/movement-cli/movement-sui/client/publish).

(Add the --skip-dependency-verification` flag in your `publish` command if prompted.)

Once the package is published, get the ID from `Transaction Data` under `Object Changes` > `Published Objects`.

We'll use `0x76f85cd75c8e7ebac57382ea08a5c90eb2bf3128e4be68710bab67c9834fd35b` here for demonstration purposes.

In `constants.ts` export `M2_COUNTER_PACKAGE_ID`:

```
export const DEVNET_COUNTER_PACKAGE_ID = "0xTODO";
export const MAINNET_COUNTER_PACKAGE_ID = "0xTODO";
export const M2_COUNTER_PACKAGE_ID = "0x76f85cd75c8e7ebac57382ea08a5c90eb2bf3128e4be68710bab67c9834fd35b"
```









