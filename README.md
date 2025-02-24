All  building is done via `anchor build -v`

## Building with default and no OFT_ID environment variable

Below is the testing log.

Used Solana 1.17

```
sh -c "$(curl -sSfL https://release.solana.com/v1.17.31/install)"
```

Built the program
```
anchor build -v
```

DID NOT change the below snippet:
```
declare_id!(Pubkey::new_from_array(program_id_from_env!(
    "OFT_ID",
    "9UovNrJD8pQyBLheeHNayuG1wJSEAoxkmM14vw5gcsTT"
)));
```

Ran:
```
solana-verify get-executable-hash target/verifiable/declare_id_test.so
```

resulted in the bytecode hash:
```
08f7db8120d707dd8cc13fdd978e3a716c628e192c405897a33e880987790ca6
```

## Building with `OFT_ID` set to `4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6`

Built with env var:
```
anchor build -v -e OFT_ID=4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6
```

and ran
```
solana-verify get-executable-hash target/verifiable/declare_id_test.so
```

resulted in the bytecode hash
```
eb26f9fbe4fe6addc2dcf54f79fcd44144851040430887d926c0cb48dd0abdf7
```

Temporarily switched to 1.18

```
sh -c "$(curl -sSfL https://release.solana.com/v1.18.26/install)"
```

Deployed program with id `4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6` to devnet

```
solana program deploy -ud target/verifiable/declare_id_test.so --program-id target/deploy/declare_id_test-keypair.json --with-compute-unit-price 400000 --max-sign-attempts 100
```

Ran solana-verify

```
solana-verify verify-from-repo -ud --library-name declare_id_test --program-id 4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6 https://github.com/nazreen/declare-id-test -- --config env.OFT_ID=\'4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6\'
```

Resulted in
```
Fetching on-chain program data for program ID: 4zWMoR3G5hhUY4V51JXvxuCw255D9zeoGRd4dBNJtma6
Executable Program Hash from repo: eb26f9fbe4fe6addc2dcf54f79fcd44144851040430887d926c0cb48dd0abdf7
On-chain Program Hash: eb26f9fbe4fe6addc2dcf54f79fcd44144851040430887d926c0cb48dd0abdf7
Program hash matches ✅
```

note: `--mount-path` needs to be specified if `Cargo.lock` is not in the repository root

note: `--remote` can only be done on mainnet


Uploading of verification data (to devnet) is a success:

```
Uploading the program verification params to the Solana blockchain...
Using connection url: https://api.devnet.solana.com
Program uploaded successfully. Transaction ID: 4eTBf3YCV5cerTd8quiwQGQJzyuSkDXuid2kfAb4ssvHKuL6Gv8XCYCoYez1xLzWxDKF3nSBrikJKoTGvqbQF27Z
```