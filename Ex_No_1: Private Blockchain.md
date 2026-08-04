EX.NO-1: Creating a Private Blockchain
AIM
To create a Private Blockchain, add nodes, create accounts, transfer Ether into it by creating and deploying a Smart Contract.

PROCEDURE
1. Install Geth
Go to https://geth.ethereum.org/
Download the Windows version.
During installation, select both Geth and Development Tools.
2. Verify Installation
Run the following command in Command Prompt:
```
geth
```
3. Create a Private Blockchain Directory
```
mkdir go-ethereum
cd go-ethereum
```
4. Create Two Nodes
```
mkdir node1
mkdir node2
```
5. Open VS Code
```
code .
```
6. Create an Account for Node1
```
cd node1
geth --datadir "./data" account new
```
Save the public address and password of Node1 in info.txt.
7. Create an Account for Node2
```
cd ..
cd node2
geth --datadir "./data" account new
```
Save the public address and password of Node2 in info.txt.
Create the Genesis Block
8. Create privateblock.json
Create a file named privateblock.json inside the go-ethereum directory.

Replace Chain ID with your own unique Chain ID.
Verify the Chain ID using https://chainlist.org/
Replace:
Initial signer address with Node1 Address
First node address with Node1 Address
Second node address with Node2 Address
Set the balance for both nodes as:
3000000000000000000
Configure Both Nodes
9. Initialize Node1
```
cd node1
geth --datadir ./data init ../privateblock.json
```
10. Initialize Node2
```
cd ../node2
geth --datadir ./data init ../privateblock.json
```
Create Bootnode
11. Create Bootnode Directory
```
mkdir bnode
cd bnode
```
12. Generate Bootnode Key
```
bootnode -genkey boot.key
bootnode -nodekey boot.key -verbosity 7 -addr "127.0.0.1:30301"
```
13. Save Enode
Copy the generated Enode URL and save it in info.txt.
Run the Nodes
14. Start Node1
```
geth --datadir "./data" \
--port 30304 \
--bootnodes "enode://YOUR_ENODE_VALUE" \
--authrpc.port 8547 \
--ipcdisable \
--allow-insecure-unlock \
--http \
--http.corsdomain="https://remix.ethereum.org" \
--http.api web3,eth,debug,personal,net \
--networkid YOUR_NETWORK_ID \
--unlock YOUR_NODE1_ADDRESS \
--password password.txt \
--mine \
--miner.etherbase YOUR_NODE1_ADDRESS
```
Start Node2
```
geth --datadir "./data" \
--port 30306 \
--bootnodes "enode://YOUR_ENODE_VALUE" \
--authrpc.port 8546 \
--networkid YOUR_NETWORK_ID \
--unlock YOUR_NODE2_ADDRESS \
--password password.txt
```
Replace:

YOUR_ENODE_VALUE → Bootnode Enode URL
YOUR_NETWORK_ID → Chain ID
YOUR_NODE1_ADDRESS → Node1 Address
YOUR_NODE2_ADDRESS → Node2 Address
Create a password.txt file inside both node1 and node2 directories and enter the respective account password.

Deploy Smart Contract
15. Open Remix IDE
https://remix.ethereum.org/

16. Select Environment
Deploy & Run Transactions
Choose Custom - External HTTP Provider
17. Create Smart Contract
Create a new file named:
```
New.sol
```
18. Deploy Contract
Save the file and click Deploy.

19. Deployment
The smart contract is deployed successfully on Node1 and added to the blockchain.


PROGRAM
#Genesis file privateblock.json
```
{
    "config":{
        "chainId":8515,
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 0,
        "eip158Block": 0,
        "byzantiumBlock": 0,
        "constantinopleBlock": 0,
        "petersburgBlock": 0,
        "istanbulBlock": 0,
        "berlinBlock": 0,
        "clique": {
          "period": 5,
          "epoch": 30000
        }
    } ,
        "difficulty": "1",
        "gasLimit": "8000000",
        "extradata": "0x000000000000000000000000000000000000000000000000000000000000000003755DDF775cD4fbe6Ef347ce22a6Ed5fbe1014F0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "alloc": {
            "03755DDF775cD4fbe6Ef347ce22a6Ed5fbe1014F": { "balance": "3000000000000000000" },
            "1cBbc951bA624b48FC6aC1A2ee8B93BbCb69F9D8": { "balance": "3000000000000000000" }
        }
 
}
```
6
#Smart Contract New.sol
```
//SPDX-License-Identifier MIT
pragma solidity ^0.8.19;
contract New{
string name;
function setName(string memory _name) public {
name= _name;
}
function getName() public view returns (string memory){
return name;
}
}
```
OUTPUT
# Deploying Transaction in Remix
<img width="1920" height="1080" alt="Screenshot 2026-08-03 081757" src="https://github.com/user-attachments/assets/66893ebf-6b04-4c8c-880d-a34b6fc61f10" />

# Contract Creation Output in Command Prompt
<img width="1920" height="1080" alt="Screenshot 2026-08-03 081740" src="https://github.com/user-attachments/assets/d00f7fb8-a9ab-4392-9e02-575c056348dd" />

RESULT: Thus, the Private Blockchain is created, nodes are added with accounts, and Ether is transferred
into it by creating and deploying Smart contract successfully
