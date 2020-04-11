# dbchain
dbChain full node provides blockchain based relational database with integrated ipfs.

## install
$ docker pull dbchain/dbchain

## config

$ sudo docker network create --subnet="172.20.0.0/16" dbcnet

$ mkdir docker_store

$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain/store dbchain/dbchain bash

In the docker client os, do the following:
  $ cp .bashrc .profile profile
  $ exit
  
$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain dbchain/dbchain bash

  $ ipfs init
  
  $ dbchaind init node01 --chain-id testnet
  
  $ dbchaincli keys add alice
  
  $ dbchaincli keys add bob
  
  $ dbchaind add-genesis-account $(dbchaincli keys show alice -a) 10000000000dbctoken,10000000000stake
  
  $ dbchaind add-genesis-account $(dbchaincli keys show bob -a) 10000000000dbctoken,10000000000stake
  
  $ dbchaind add-genesis-admin-account $(dbchaincli keys show alice -a)
  
  $ dbchaind add-genesis-admin-account $(dbchaincli keys show bob -a)
  
  $ dbchaincli config chain-id testnet
  
  $ dbchaincli config output json
  
  $ dbchaincli config indent true
  
  $ dbchaincli config trust-node true
  
  $ dbchaind gentx --name alice
  
  $ dbchaind collect-gentxs

  $ dbchaind validate-genesis
  
  $ exit
  
## run

$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain dbchain/dbchain


