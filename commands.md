# Developer Commands

```sh
yarn
mkdir -p target/deploy
cp -r tests/test-keypairs/* target/deploy

find . -type f -name "*" | xargs sed -i .bak "s/stkBL96RZkjY5ine4TvPihGqW8UHJfch2cokjAPzV8i/$(solana-keygen pubkey tests/test-keypairs/cardinal_stake_pool-keypair.json)/g"

find . -type f -name "*" | xargs sed -i .bak "s/rwdNPNPS6zNvtF6FMvaxPRjzu2eC51mXaDT9rmWsojp/$(solana-keygen pubkey tests/test-keypairs/cardinal_reward_distributor-keypair.json)/g"

find . -type f -name "*.bak" | xargs rm

sh -c "$(curl -sSfL https://release.solana.com/v1.9.13/install)"

solana-test-validator --url https://api.devnet.solana.com --clone metaqbxxUerdq28cj1RbAWkYQm3ybzjb6a8bt518x1s --clone PwDiXFxQsGra4sFFTT8r1QWRMd4vfumiWC1jfWNfdYT --clone mgr99QFMYByTqGPWmNqunV7vBLmWWXdSrHUfV8Jf3JM --clone ojLGErfqghuAqpJXE1dguXF7kKfvketCEeah8ig6GU3 --reset & echo $$! > validator.PID

solana airdrop 1000 $(solana-keygen pubkey tests/test-key.json) --url http://localhost:8899

anchor test --skip-local-validator --provider.cluster localnet
anchor run test-s
```
