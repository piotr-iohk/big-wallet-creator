# big-wallet-creator

A helper script to aid testing of cardano-wallet-backends on top of testnets and get some stats about them.

```
Big wallets creator

Usage:
  ./script.rb [--conf=<co>] stats (new|old) [full] [<wid>]
  ./script.rb [--conf=<co>] stats jorm [stake] [logs]
  ./script.rb [--conf=<co>] test <wid1> <wid2> 
  ./script.rb [--conf=<co>] tx <wid1> <wid2> 
  ./script.rb config read [--conf=<co>]
  ./script.rb config gen [--conf=<co>] [--max-sleep=<sec>] [--max-tx-spend=<t>] [--port-old=<port>] [--port-new=<port>] [--port-jorm=<port>] 
  ./script.rb -h | --help

Args:
  stats (new|old)     Stats for new or old wallet
  stats jorm          Stats for Jormungandr node
  test                Run txs between 2 wallets <wid1> <wid2>
  tx                  Run 1 tx between 2 wallets <wid1> <wid2>
  config              Read or gen config file
  
Options:
  -h --help           Show this screen. 
  --conf=<co>         Path to config file [default: ./config.yml]
  --max-sleep=<sec>   Max sleep between two txs when testing [default: 5]
  --max-tx-spend=<t>  Max tx spend between two txs when testing [default: 0.00001]
  --port-old=<port>   Old wallet's server port [default: 46083]
  --port-new=<port>   New wallet's server port [default: 8090]
  --port-jorm=<port>  Jormungandr node api port [default: 8080]
  ```
