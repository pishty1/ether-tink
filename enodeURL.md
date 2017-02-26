Connection procedure:

Overview.

 - Raspberry pi with dhcp server, ip address 192.168.0.1
 - Geth node initiated using genesis.json
 

1. Establish ethernet connection to pi - connect cable to switch (or wifi to router) and make sure network interface "obtains IP address automatically" in adapter settings.
2. Install go-ethereum or other client
3. On command line, geth init /path/to/your/genesis.json
   this initialises the first block. you are now primed to connected to the p2p network
4. now do;
       `geth --networkid 12345 --port 33333 --verbosity 5`
  this will give lots of messages about the network and what is going on
5.next, in a new command window (leave the other one open
       `geth attach`
  this should result it a `>` prompt
6. next do:
       `admin.addPeer("enode://6c461262a4cdb658d7852af41a433668dea467da87168390d02e22c6191fc136063a7df859e46a65786de6c3f73670f00d2378b5e17ec3142a84ded8029e1728@192.168.0.133333")`
  this results in a connection to the RPi - you've found the network check your firewall if not (allow connections on TCP port 33333)
7. do `admin.peers` to check
8. `personal.newAccount("yourPassword")` to create a new accoount - it will give you a hex format accnt no
9. `miner.setEtherbase("yourAccount")`
10 `miner.start()`
    this will start mining, with the rewards going to your account

