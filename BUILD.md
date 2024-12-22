# Continue building locally

Projects deployed through ICP Ninja are temporary; they will only be live for 20 minutes before they are removed. The command-line tool `dfx` can be used to continue building your ICP Ninja project. `dfx` can be used to deploy projects to the mainnet for long-term production use. It is designed specifically for building ICP smart contracts and supports every feature of the network.

To migrate your ICP Ninja project off of the web browser and develop it locally, follow these steps.

### 1. Install developer tools.

You can install the developer tools natively or develop using Dev Containers.

#### Option 1: Natively install developer tools

> Installing `dfx` natively is currently only supported on macOS and Linux systems. On Windows, it is recommended to use Dev Containers below.

1. Install `dfx` with the following command:

```
sh -ci "$(curl -fsSL https://internetcomputer.org/install.sh)"
```

2. [Install NodeJS](https://nodejs.org/en/download/package-manager).

> On Apple Silicon (e.g., Apple M1 chip), make sure you have Rosetta installed (`softwareupdate --install-rosetta`).

3. For Rust projects, you will also need to:

- Install [Rust](https://doc.rust-lang.org/cargo/getting-started/installation.html#install-rust-and-cargo): `curl https://sh.rustup.rs -sSf | sh`
- Install [candid-extractor](https://crates.io/crates/candid-extractor): `cargo install candid-extractor`

4. For Motoko projects, you will also need to:

- Install the Motoko package manager [Mops](https://docs.mops.one/quick-start#2-install-mops-cli): `npm i -g ic-mops`

Lastly, navigate into your project's directory that you downloaded from ICP Ninja.

#### Option 2: Dev Containers

Continue building your projects locally by installing the [Dev Container extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) in VS Code and [Docker](https://docs.docker.com/engine/install/).

Make sure Docker is running, then navigate into your project's directory that you downloaded from ICP Ninja and start the Dev Container by selecting `Dev-Containers: Reopen in Container` in VS Code's command palette (F1 or Ctrl+Shift+P).

### 2. Create a local developer identity.

To manage your project's canisters, it is recommended that you create a local [developer identity](https://internetcomputer.org/docs/current/developer-docs/getting-started/accounts) rather than use the `dfx` default identity that is not stored securely.

To create a new identity, run the commands:

```
dfx start --background
dfx identity new IDENTITY_NAME
dfx identity use IDENTITY_NAME
```

Replace `IDENTITY_NAME` with your preferred identity name. The first command, `dfx start --background` starts the local `dfx` processes, then `dfx identity new` will create a new identity and return your identity's seed phase. Be sure to save this in a safe, secure location.

The third command, `dfx identity use` will tell `dfx` to use your new identity as the active identity. Any canister smart contracts created after running `dfx identity use` will be owned and controlled by the active identity.

Your identity will have a **principal ID** associated with it. Principal IDs are used to identify different entities on ICP, such as users and canisters.

[Learn more about ICP developer identities](https://internetcomputer.org/docs/current/developer-docs/getting-started/accounts).

### 3. Deploy the project locally.

Deploy your project to your local developer environment with the commands:

```
dfx deploy
```

Your project will be hosted on your local machine. The local canister URLs for your project will be shown in the terminal window as output of the `dfx deploy` command. You can open these URLs in your web browser to view the local instance of your project.

### 4. Obtain cycles.

To deploy your project to the mainnet for long term, public accessability, first you will need **[cycles](https://internetcomputer.org/docs/current/developer-docs/getting-started/cycles/overview)**. Cycles are used to pay for the resources your project uses on the mainnet, such as storage and compute.

> This cost model is known as ICP's [reverse gas model](https://internetcomputer.org/docs/current/developer-docs/gas-cost), where developers pay for their project's gas fees rather than users pay for their own gas fees. This model provides an enhanced end user experience since they do not need to hold tokens or sign transactions when using a dapp deployed on ICP.
> Learn how much a project may cost by using the [pricing calculator](https://internetcomputer.org/docs/current/developer-docs/cost-estimations-and-examples).

Cycles can be obtained through:

- [Requesting a free cycles coupon](https://internetcomputer.org/docs/current/developer-docs/getting-started/cycles/cycles-faucet).

- [Converting ICP tokens into cycles using `dfx`](https://internetcomputer.org/docs/current/developer-docs/developer-tools/cli-tools/cli-reference/dfx-cycles#dfx-cycles-convert).

### 5. Deploy to the mainnet.

Once you have cycles to deploy your project to the mainnet, run the command:

```
dfx deploy --network ic
```

After your project has been deployed to the mainnet, it will continuously require cycles to pay for the resources it uses. You will need to [top up](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/topping-up/topping-up-canister) your project's canisters or set up automatic cycles management through a service such as [CycleOps](https://cycleops.dev/).

> If your project's canisters run out of cycles, they will be removed from the network.

## Next steps

Once your project has been deployed using `dfx`, you may want to learn about:

- [Making calls to canisters](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/call/overview).

- [Controlling a canister](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/maintain/control).

- [Canister logging](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/maintain/logs).

- [Canister settings](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/maintain/settings).

- Advanced features such as [Chain Fusion](https://internetcomputer.org/docs/current/developer-docs/multi-chain/overview), [randomness](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/advanced-features/randomness), [onchain signatures](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/signatures/t-ecdsa), or [timers](https://internetcomputer.org/docs/current/developer-docs/smart-contracts/advanced-features/periodic-tasks).

## Additional examples

Additional code examples and sample applications can be found in the [DFINITY examples repo](https://github.com/dfinity/examples).
