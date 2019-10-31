# big-wallet-creator

A helper script to aid testing of cardano-wallet-backends on top of testnets and get some stats about them.

### To start using
1. Have [Ruby](https://www.ruby-lang.org/en/downloads/).
2. :point_down:
```
git clone https://github.com/piotr-iohk/big-wallet-creator.git
cd big-wallet-creator
bundle install
./wa config gen      # generates script's config.yml with default values
```

### Config
Edit generated config file directly or by using `wa config gen...`
```
---
:port_new: '8090'
:pass_new: Secure Passphrase
:port_jorm: '8080'
:max_tx_spend: 0.001
:max_sleep: 0
```
**Note:** About `max_tx_spend`... the script uses it to select random amount for transaction (when using `tx` or `test`), like `[*1...max_tx_spend*available_balance].sample`. So if the wallet balance is big, consider having `max_tx_spend` very small (otherwise the generation of sample takes a lot of time...). On the contrary, if the balance is small, consider having `max_tx_spend` bigger (for having nicer amounts to send).

### To use

```
$ ./wa --help

Wallet test aid

Usage:
  ./wa [--conf=<co>] stats (new|old) [full] [<wid>]
  ./wa [--conf=<co>] stats jorm [stake] [logs]
  ./wa [--conf=<co>] del-all (new|old)
  ./wa [--conf=<co>] test [same_addr] <wid1> <wid2> 
  ./wa [--conf=<co>] tx <wid1> <wid2> 
  ./wa config read [--conf=<co>]
  ./wa config gen [--conf=<co>] [--max-sleep=<sec>] [--max-tx-spend=<t>] [--port-new=<port>] [--pass-new=<pass>] [--port-jorm=<port>] 
  ./wa -h | --help

Args:
  stats (new|old) Stats for new wallet or old wallet
  stats jorm            Stats for Jormungandr node
  test [same_addr]      Run txs back and forth between 2 wallets <wid1> <wid2>
                        if same_addr provided uses the same address all the time, 
                        otherwise always picks some unused one
  tx                    Run 1 tx between 2 wallets <wid1> <wid2>
  del-all               Delete all new wallets
  config                Read or gen config file
  
Options:
  -h --help           Show this screen. 
  --conf=<co>         Path to config file [default: ./config.yml]
  --max-sleep=<sec>   Max sleep between two txs when testing [default: 0]
  --max-tx-spend=<t>  Max tx spend between two txs when testing [default: 0.00001]
  --port-new=<port>   New wallet's server port [default: 8090]
  --pass-new=<pass>   Password for new wallet [default: Secure Passphrase]
  --port-jorm=<port>  Jormungandr node api port [default: 8080]
  ```
