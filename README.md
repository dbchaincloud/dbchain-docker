# dbchain
dbChain full node provides blockchain based relational database with integrated ipfs.

## install
```shell
$ docker pull dbchain/dbchain
```

## config
```shell
$ sudo docker network create --subnet="172.20.0.0/16" dbcnet

$ mkdir docker_store

$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain/store dbchain/dbchain bash
```

In the docker client os, do the following:

```shell
  $ cp .bashrc .profile store
  $ exit
```  
  
Then run the follow command to get in the container bash
```shell
$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain dbchain/dbchain bash
```
In the container bash, run the follow commands
```shell
  $ ipfs init
  $ dbchaind init node01 --chain-id testnet
  $ dbchaincli keys add alice
  $ dbchaincli keys add bob
  $ dbchaind add-genesis-account $(dbchaincli keys show alice -a) 10000000000dbctoken,10000000000stake
  $ dbchaind add-genesis-account $(dbchaincli keys show bob -a)   10000000000dbctoken,10000000000stake
  $ dbchaind add-genesis-admin-account $(dbchaincli keys show alice -a)
  $ dbchaind add-genesis-admin-account $(dbchaincli keys show bob -a)
  $ dbchaincli config chain-id testnet
  $ dbchaincli config output json
  $ dbchaincli config indent true
  $ dbchaincli config trust-node true
  $ dbchaind gentx --name alice
  $ dbchaind collect-gentx
  $ dbchaind validate-genesis
  $ exit
```  
## run
After the above configuring, it's time to start the full node
```shell
$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain dbchain/dbchain
```

