# big-wallet-creator

A helper script to aid testing of cardano-wallet-backends on top of testnets and get some stats about them.

### To start using

#### Linux

1. Have [ruby](https://www.ruby-lang.org/en/downloads/), e.g.:

```
sudo apt-get install ruby
```
or
```
yum install ruby
```
2. :point_down:
```
git clone https://github.com/piotr-iohk/big-wallet-creator.git
cd big-wallet-creator
bundle install
./wa config gen      # generates script's config.yml with default values
```

#### Windows
1. Have [ruby](https://www.ruby-lang.org/en/downloads/) and git, e.g.:
```
choco install ruby
choco install git
```
2. :point_down:
```
git clone https://github.com/piotr-iohk/big-wallet-creator.git
cd big-wallet-creator
bundle install
ruby wallet-aid config gen      # generates script's config.yml with default values
```

### Config
Edit generated config file directly or by using `./wa config gen...` (`ruby wallet-aid config gen...`)
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
  ./wa [--conf=<co>] stats stake-pools
  ./wa [--conf=<co>] stats jorm [stake] [logs]
  ./wa [--conf=<co>] create (new|old) <name>
  ./wa [--conf=<co>] create-many (new|old) <number>
  ./wa [--conf=<co>] del (new|old) <wid>
  ./wa [--conf=<co>] del-all (new|old)
  ./wa [--conf=<co>] test [same_addr] <wid1> <wid2> 
  ./wa [--conf=<co>] tx <wid1> <wid2>
  ./wa [--conf=<co>] join-sp <sp_id> <wid>  
  ./wa config read [--conf=<co>]
  ./wa config gen [--conf=<co>] [--max-sleep=<sec>] [--max-tx-spend=<t>] [--port-new=<port>] [--pass=<pass>] [--port-jorm=<port>] 
  ./wa -h | --help

Args:
  stats (new|old)        Stats for new wallet (Shelley) or old wallet (Byron)
  stats stake-pools      List stake pools via wallet backend
  stats jorm             Stats for Jörmungandr node
  test [same_addr]       Run txs back and forth between 2 wallets <wid1> <wid2>
                         if same_addr provided uses the same address all the time, 
                         otherwise always picks some unused one
  tx                     Run 1 tx between 2 wallets <wid1> <wid2>
  create (new|old)       Create new wallet (Shelley) or old wallet (Byron)
  create-many (new|old)  Create many wallets (Shelley or Byron)
  del (new|old)          Delete new wallet (Shelley) or old wallet (Byron)
  del-all (new|old)      Delete all new wallets (Shelley) or old wallets (Byron)
  join-sp <sp_id> <wid>  Join stake-pool identified by stake-pool id <sp_id> 
                         with your wallet identified by wallet id <wid>
  config                 Read or gen config file
  
Options:
  -h --help           Show this screen. 
  --conf=<co>         Path to config file [default: ./config.yml]
  --max-sleep=<sec>   Max sleep between two txs when testing [default: 0]
  --max-tx-spend=<t>  Max tx spend between two txs when testing [default: 0.00001]
  --port-new=<port>   New wallet's server port [default: 8090]
  --pass=<pass>       Password for wallets [default: Secure Passphrase]
  --port-jorm=<port>  Jormungandr node api port [default: 8080]

  ```
