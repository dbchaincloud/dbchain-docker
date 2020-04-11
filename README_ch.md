[English](https://github.com/dbchaincloud/dbchain/blob/master/README.md)

# 库链
库链全节点提供基于区块链的关系数据库，并高度集成了ipfs作为联盟链的分布式存储。为区块链应用提供了完整解决方案。 

## 安装 
```shell
$ docker pull dbchain/dbchain
```

## 配置 
```shell
$ sudo docker network create --subnet="172.20.0.0/16" dbcnet

$ mkdir docker_store

$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain/store dbchain/dbchain bash
```

在docker容器环境里，运行如下命令:

```shell
  $ cp .bashrc .profile store
  $ exit
```  
然后用下面的命令重新进入容器:

```shell
$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -v $(pwd)/docker_store:/home/dbchain dbchain/dbchain bash
```
在容器里，运行下面命令:

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
  $ dbchaind collect-gentxs
  $ dbchaind validate-genesis
  $ exit
```  
## 运行
在完成上面的配置工作后，现在启动库链全节点:

```shell
$ sudo docker run --net dbcnet --ip 172.20.0.101 --user 1000:1000 -it -d -v $(pwd)/docker_store:/home/dbchain dbchain/dbchain
```
