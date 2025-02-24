All  building is done via `anchor build -v`

## Building with default and no OFT_ID environment variable

```
anchor build -v
```

```
declare_id!(Pubkey::new_from_array(program_id_from_env!(
    "OFT_ID",
    "9UovNrJD8pQyBLheeHNayuG1wJSEAoxkmM14vw5gcsTT"
)));
```

and running
```
solana-verify get-executable-hash target/verifiable/declare_id_test.so
```

results in the bytecode hash:
```
08f7db8120d707dd8cc13fdd978e3a716c628e192c405897a33e880987790ca6
```

## Building with `OFT_ID` set to `4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6`

```
OFT_ID=4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6 anchor build -v
```

and running
```
solana-verify get-executable-hash target/verifiable/declare_id_test.so
```

results in the bytecode hash
```

```

Deployed program with id `4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6` to devnet

```
solana program deploy -ud target/verifiable/declare_id_test.so --program-id target/deploy/declare_id_test-keypair.json --with-compute-unit-price 400000 --max-sign-attempts 100
```

Running solana-verify

```
solana-verify verify-from-repo --remote -um --mount-path examples/oft-solana/programs/oft --library-name dvn --program-id 4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6 https://github.com/LayerZero-Labs/devtools -- --config env.OFT_ID=\'4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6\'
```