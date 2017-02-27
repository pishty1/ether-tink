#Ethereum Private Blockchain Tinkering:

Guidlines for getting connected to the private network.

##Overview.

 The network consists of Raspberry pi with dhcp server (ip address `192.168.0.1`) running a go-ethereum node initated with the `genesis.json` file.
 The intent is to create a network of local computers over which a private blockchain can be created. To help do this, follow the guidance below for different clients:
 
 ###Go-ethereum "geth":
 
1. Install go-ethereum or other client; https://ethereum.github.io/go-ethereum/install/
2. Establish ethernet connection to pi - connect cable to switch (or wifi to router) and make sure network interface "obtains IP address automatically" in your adapter settings.
3. On command line run, `geth init /path/to/your/genesis.json`
   *This initialises the first block. you are now primed to connected to the p2p network*
4. Now do:
       `geth --networkid 12345 --port 33333`
   *This connects establishes the link (TCP) for your machine in the local network. The networkid and port were arbitrarily chosen when I set up the pi. N.b. `--verbosity 5`  will give lots of messages about the network and what is going on.*
5. Next, in a new command window (leave the other one open):
       `geth attach`
  *This gives you a javascript console to interact with; a `>` prompt*
6. Next do:
       `admin.addPeer("enode://6c461262a4cdb658d7852af41a433668dea467da87168390d02e22c6191fc136063a7df859e46a65786de6c3f73670f00d2378b5e17ec3142a84ded8029e1728@192.168.0.133333")`
  This creates the first Peer to Peer link  this results in a connection to the RPi - you've found the network check your firewall if not (allow connections on TCP port 33333)
7. do `admin.peers` to check
8. `personal.newAccount("yourPassword")` to create a new accoount - it will give you a hex format accnt no
9. `miner.setEtherbase("yourAccount")`
10 `miner.start()`
    this will start mining, with the rewards going to your account

