# tzBTC-client
## Preparation
Install [Nix package manager ](https://nixos.org/nix/manual/#ch-installing-binary) and [Haskell Tool Stack](https://docs.haskellstack.org/en/stable/install_and_upgrade/)

## Downloading tzbtc-client source code
Download [latest released version](release/)

## Prerequisites

In order to use `tzbtc-client` you will need to obtain `tezos-client`
executable. `tezos-client` is used for key storing, operation signing and ledger interaction.
For now, `tezos-client` doesn't support packed value signing via ledger,
so in order to fully use `tzbtc-client` (perform multisig package signing via ledger)
you should use patched `tezos-client` binary. 

You can build patched binary using nix.

In order to do that you should run one of the following command:
```
nix-build release.nix -A tezos-client -o tezos-client
```
Thus `tezos-client` directory will have statically built binary which can be used later.

If you are not going to use multisig package signing with ledger device,
you can obtain non-patched version of `tezos-client` in various form of distribution from
[tezos-packaging repo](https://github.com/serokell/tezos-packaging).

## Building instruction for tzbtc-client
You can build `tzbtc-client` and `tzbtc` from the sources.

There are two ways:
* Build stack project `stack build`, thus you'll be able to run executables using `stack exec tzbtc` or `stack exec tzbtc-client`. Also you can use `stack install tzbtc --local-bin-path ./bin`, thus `tzbtc-client` and `tzbtc` binaries will be in `./bin` directory. 
* Build static binaries from the stack project using nix. For this you will need to run:
``` bash
$(nix-build --no-link -A fullBuildScript) -o ./tzbtc-static
```
Static binaries will be located in `./tzbtc-static/bin` directory.

In case you are facing memory problems:
- try increasing the memory in case you are working in a VM and / or
- try building with `stack build -j1 --fast`
