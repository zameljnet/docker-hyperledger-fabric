docker-hyperledger-fabric
====
docker-hyperledger-fabric-v1.2
Fabric v1.2.0	latest stable fabric 1.2.0 release.

#Getting Started


###Quick Test
The following command will run the entire process (start a fabric network, create channel, test chaincode and stop it.
---bash
$ make setup download # Install docker/compose, and pull required images
$ make test  # Test with default fabric solo mode
---

##Test with more modes

$ HLF_MODE=solo make test # Bootup a fabric network with solo mode
$ HLF_MODE=couchdb make test # Enable couchdb support, web UI is at `http://localhost:5984/_utils`
$ HLF_MODE=event make test  # Enable eventhub listener
$ HLF_MODE=kafka make test # Bootup a fabric network with kafka mode
$ HLF_MODE=be make test  # Start a blockchain-explorer to view network info

###To Start a Fabric network

$ make stop
$ make clean 
$ make startFabric

##More Details
more details can be seen in your makefile

##Environment Setup

The following scripts will setup the environment by installing Docker, Docker-Compose and download required docker images.

$ make setup # setup environment

##Generate crypto-config and channel-artifacts

$ make gen_config
The cmd actually calls scripts/gen_config.sh to generate the crypto-config and channel-artifacts.

##Bootup Fabric Network

Start a 4 peer (belonging to 2 organizations) fabric network.

$ make start  # Start a fabric network
The script actually uses docker-compose to boot up the fabric network with several containers.

There will be 7 running containers, include 4 peers, 1 cli, 1 ca and 1 orderer.

##Create Application Channel

$ make test_channel_create 
The command actually calls the scripts/test_channel_create.sh script in the fabric-cli container, to create a new application channel with default name of businesschannel.

##Join Peers into Application Channel

$ make test_channel_join 
The command actually calls the scripts/test_channel_join.sh script in the fabric-cli container, to join all peers into the channel.

##Intall Chaincode to All Peers

$ make test_cc_install
The command actually calls the scripts/test_cc_install.sh script in the fabric-cli container, to install chaincode example02 for testing.

##Instantiate Chaincode in the Application Channel

$ make test_cc_instantiate
The command actually calls the scripts/test_cc_instantiate.sh script in the fabric-cli container, to instantiate chaincode example02.

And there will be new chaincode container generated in the system

##Test Chaincode

$ make test_cc_invoke_query
The command actually calls the scripts/test_cc_invoke_query.sh script in the fabric-cli container, to test chaincode example02 with invoke and query.

##Test System Chaincode

$ make test_lscc # test LSCC
$ make test_qscc # test QSCC
The command actually calls the scripts/test_lscc.sh and scripts/test_qscc.sh script in the fabric-cli container, to test LSCC and QSCC.

##Test Fetch Blocks

$ make test_fetch_blocks # test fetch blocks
The command actually calls the scripts/test_fetch_blocks.sh script in the fabric-cli container, to test fetching blocks from channels.

##Test Configtxlator

$ make test_configtxlator
The command actually calls the scripts/test_configtxlator.sh script in the fabric-cli container, to test configtxlator to change the channel configuration.

More details can be found at Configtxlator.

##Stop the network

$ make stop # stop the fabric network
Clean environment

##Clean all related containers and images.

$ make clean # clean the environment

