# Admin Usage

## Prepare a Transaction

For simplicity, you can import public keys of your members with aliases like so:

 ```sh
 tezos-client import public key <alias> <key>
 # tezos-client import public key alice edpk.....
 ```

Prepare a transaction on your multisig contract named `msig` transferring 10 XTZ to an address aliases by the name `bob`:

```
tezos-client prepare multisig transaction on msig transferring 10 to bob
```

The result may look something like:

```
0x05070707070a00000004af1864d90a003d036d0743036e0a00000016000001601b92e387b8000655036a0000000a24f92abf808cc7269e0c8b2b7fbb8d7f04db000707000005050200000063020000005e03200519d0229c926b9209da439da2e59e33374443357365745f7072696365072f02000000080743035b0010032702000000000743036a00000743036a0080def368034d031b
```

The resul is a set of bytes that will need to be signed by at least the threshold of the members of `msig`. Distribute these bytes, direct the members to sign, and then get ready to submit the action to the blockchain.


## Sign a Transaction

What will be run by each member.

```
tezos-client -E https://mainnet.smartpy.io sign bytes '0x05070707070a00000004af1864d90a003d036d0743036e0a00000016000001601b92e387b8000655036a0000000a24f92abf808cc7269e0c8b2b7fbb8d7f04db000707000005050200000063020000005e03200519d0229c926b9209da439da2e59e33374443357365745f7072696365072f02000000080743035b0010032702000000000743036a00000743036a0080def368034d031b' for <key-name>
```

This will return a signature value such as:

```
edsigtZvK3uaWnc6twht2Vo8hJVuhsaCwzD7LPbGCcpAwabe8vojcg8Tp3grxtFw1UZ6HDgYes6ujjwsD1rjRMuV9s3PnkVbcgZ
```

Have each member send you their signature!

## Submit a Transaction

Assuming you've recieved signature values from `alice` and you are `charlie`, you can submit the transaction as follows:

```sh
tezos-client from multisig contract msig transfer 10 to bob on behalf of charlie with signatures "edsig-alice-sig" "edsig-charlie-sig"
```

Success!