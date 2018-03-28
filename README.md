# Setting up private POA (Proof-of-Authority ) blockchain : Ethereum

#### Follow the steps to setup and run a POA chain
Credits: [Salanfe][credit1]

##### Set up accounts

```sh
geth --datadir node1/ account new
geth --datadir node2/ account new
```

##### Copy the addresses and store in a file: accounts.txt

```
echo 'node1: 6e5fe920f401bd53a1878ebc1642921d2ad9b4b6' >> accounts.txt
echo 'node2: 1046fb3b698f593d5b9ee9dc240602bda06fe293' >> accounts.txt
```

#####  Store passwords for account in a file:

```
echo '1' node1/password.txt
echo '1' > node2/password.txt
```

##### Create a genesis file 
Create Genesis file using puppeth (or use the same as here). Just make sure to have some prefunded ethers to your accounts

##### Initialize nodes:

```
geth --datadir node1/ init genesis.json
geth --datadir node2/ init genesis.json
```

##### Create bootnode

```
bootnode -genkey boot.key
```

##### Script running of boot-node

```
bootnode -nodekey boot.key -verbosity 9 -addr :30310
```

##### In other terminal:

```
geth --datadir node1/ --syncmode 'full' --port 30311 --rpc --rpcaddr 'localhost' --rpcport 8501 --rpcapi 'personal,db,eth,net,web3,txpool,miner' --bootnodes 'enode://3ec4fef2d726c2c01f16f0a0030f15dd5a81e274067af2b2157cafbf76aa79fa9c0be52c6664e80cc5b08162ede53279bd70ee10d024fe86613b0b09e1106c40@127.0.0.1:30310' --networkid 1515 --gasprice '1' -unlock '0x6e5fe920f401bd53a1878ebc1642921d2ad9b4b6' --password node1/password.txt --mine
```
* Replace --bootnode value with response returned by step 8. Do not forget to replace [::] with your ip.
* Replace --unlock value by your node 1 account
* Do not forget to append 0x before the address.

##### In 3rd terminal
```
geth --datadir node2/ --syncmode 'full' --port 30312 --rpc --rpcaddr 'localhost' --rpcport 8502 --rpcapi 'personal,db,eth,net,web3,txpool,miner' --bootnodes 'enode://3ec4fef2d726c2c01f16f0a0030f15dd5a81e274067af2b2157cafbf76aa79fa9c0be52c6664e80cc5b08162ede53279bd70ee10d024fe86613b0b09e1106c40@127.0.0.1:30310' --networkid 1515 --gasprice '0' --unlock '0x1046fb3b698f593d5b9ee9dc240602bda06fe293' --password node2/password.txt --mine
```

* Replace --bootnode value with response returned by step 8. Do not forget to replace [::] with your ip.
* Replace --unlock value by your node 1 account.
* Do not forget to append 0x before the address.

##### Send Transaction and enjoy POA chain. 
[credit1]: <https://hackernoon.com/setup-your-own-private-proof-of-authority-ethereum-network-with-geth-9a0a3750cda8>

