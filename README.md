# Tezos Multisig Helper

This project serves as a reference to use the [Tezos multisig](https://tezos.gitlab.io/user/multisig.html) with some helpful end-user documentation.

# What's a Multisig?

A multisig on Tezos is a smart contract that provides a mechanism to secure access to a Tezos contract using multiple parties. The parties are configurable, meaning there can be any number of members in a multisig, with any threshold necessary for an operation to success. An example could be a multisig with five members, needing only three to ‘sign off’ on an operation. This means operations in the contract — normally sending funds to another wallet, or interacting with another contract — require quorum from the signatories on the wallet. 

In joining and using a multisig you’ll need to provide information about your public key associated with your Tezos wallet, and submit a signed operation signed by your Tezos wallet. Sending your public key is safe, and carries no risk. Sending signed operations is a bit more sensitive. Never send or reveal your private or secret keys to anyone!

# Background

We assume there are two main classes of users for a multisig: an _administrator_ and a _member_. Realistically, the parties are interchangeable and have the same set of permissions; however, for simplicity it may work best to have one member take on coordination and execution functions under the title _administrator_.

We assume that there is an _administrator_ responsible for setting up the multisig and submitting operations to it after collecting the requisite number of signatures from its _members_.

# Getting a Wallet

For high security, we recommend using a hardware wallet for a multisig. Our instructions thus far are focused on [Ledger](https://www.ledger.com/) hardware wallets, though there are other options, such as a [Trezor](https://trezor.io/).

If you do not have access to a hardware wallet you may use a "hot" wallet such as those provided by [Kukai](kukai.app), [Temple](https://templewallet.com/), and others.

# Setup

For all users...

1. Install a [tezos-client](https://tezos.gitlab.io/introduction/howtouse.html)

2. Create a wallet, and get its public key

If you don't know your public key, you can view it using the `tezos-client`. First, you'll either need to import a reference to your hardware wallet, or import the secret key directly. Hardware wallet instructions can be found in the [user docs](user_docs.md). For a hot wallet, you can import your secret key as follows:

After revealing your secret key (e.g. in Temple go to Settings -> Reveal Private Key).

```sh
$ tezos-client import secret key <account_alias> unencrypted:<your_secret_key>

```

After importing your secret key or key via a ledger, you can view your public key as such:

```sh
tezos-client show address <account_alias>
```

It'll likely begin with `edpk...`.

3. Discuss the details of the multisig as a group: the funding of the multisig, the members, the threshold for signing, and who will be the admin.


## Admin-Specific Setup

Once you install a [tezos-client](https://tezos.gitlab.io/introduction/howtouse.html) you can view the multisig command options with `tezos-client man multisig`.

You'll need to deploy a new multisig, choosing the members (keys), number of required signatories (threshold), initial token balance in the multisig (qty), and where the funds are to be taken from (src).

A template deploy command is as follows:

```sh
tezos-client -E https://mainnet.smartpy.io deploy multisig <new_multisig> transferring <qty> from <src> with threshold <threshold> on public keys [<key>...] [--fee <amount>]
```

# Usage

## Admin Usage

Admin usage is mostly covered by the [official documentation](https://tezos.gitlab.io/user/multisig.html), which is [detailed here](admin_usage.md) in similar terms.


## Member Usage

Now that you've set up a multisig contract and have configured the CLI you need participants to use it properly! How does that work? Check out [the member usage documentation here](member_usage.md). The docs are focused on a user setting up a Ledger hardware wallet with a multisig for added security.