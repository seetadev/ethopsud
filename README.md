# PropTech: Registration Management and Transfer, Home Maintenance and Cleaning Planner for Elderly and Aged People

Registration Management Module: https://github.com/seetadev/ethopsud/tree/main/PropTech-Modules/Registration-Management

A distributed application to register users and properties and handle transfer of properties among users and validate.

Running the project in a development environment
Requirements
Truffle - to compile and deploy contracts
Ganache/Test-RPC - to run local development ethereum network
npm - to run the project
Metamask - ethereum wallet (browser extension)

### Setup
1. Start ganache/test-rpc on port *8545*
    * By default ganache starts on port 7545
    * If so, goto settings and change port to 8545
    * Hit restart
2. In browser connect Metamask to local network on port *8545* and log in
4. Import first five accounts from local blockchain network -
    * Copy private key of first account from ganche/test-rpc
    * In Metamask => import accounts , select private key
    * Paste the private key and press import
    * You should see Account\# with some ethereum
    * If running the project for first time
      * Goto Settings and reset account
      * This should clear any old transactions linked to the account
      * Without this step you might see Incorrect nonce error in console
    * Similarly import at least one more account from Ganache/test-rpc
5. Migrate contracts to local ethereum network using truffle
    1. On linux ```truffle migrate --development --reset```
    2. On windows ```truffle.cmd migrate --development --reset```
    3. The first account visible in ganche/test-rpc will be the *Owner* of the contract 
    
After successful setup with no errors the project can be started by running
```npm run dev```
If missing module errors come up try again after running ```npm install```
After running the server sucessfully the DAPP can be accessed on localhost:3000

## Flow of the DAPP
The purpose of the DAPP is to enable users to register themselves as well as their properties in a decentralized manner. An individual can be identified by her _SSN_ and a property by _Property Registry Number_ both of which for now are integers between 0 and 65535 (16 bit integers). 

1. Every _SSN_ or individual is associated to an address of an individual ethereum account. 
      * Any activity of registering a property or transffering a property belonging to the _SSN_ must be submitted from the registered account only.
      * An _SSN_ can be registered to an address by entering the _SSN_ in the SSN input field under heading *Individual Registry*
      * On clicking _Register_ button Metamask will prompt to submit transaction, hit submit.
        * If transcation succeeds Metamask will notify the user.
        * If transaction fails with a propmt "Identity Mismatch" it means that the supplied _SSN_ is already registered with a differnt account than the one open in Metamask currently. This error is not treated as a failed transaction, thus ether will be charged as for a successful transaction.
2. Every _Property Registry Number_ or property is associated with an _SSN_, the _SSN_ must be previously registered under *Individual Registry*
      * A _Property Registry Number_ can be registered with an _SSN_ under heading *Property Registry*
      * On clicking _Register_ button Metamask will prompt to submit the transaction, hit submit.
        * If transaction fails with a proppt "Identity Mismatch" it means that the _SSN_ supplied is not registered with the account currently open in Metamask.
        * If transaction fails with a prompt "Property Mismatch" it means that the _Property Registry Number_ supplied is already registered to some other SSN or individual.
        * Both the above errors are not treated as failure so ethers will be charged as for successful transactions.
3. Transferring _Property Registry Number_ from _Seller_ to _Buyer_
      * This transaction must be initiated while the account of the seller is logged in Metamask i.e. transfer is initiated by the seller
      * Supply the _Seller_ SSN and the _Buyer_ SSN along with the _Property Registry Number_ to transfer
      * On clicking _Transfer_ button Metamask will prompt to submit the transaction, hit submit.
        * If transaction fails with a proppt "Identity Mismatch" it means that the _SSN_ supplied is not registered with the account currently open in Metamask.
        * If transaction fails with a prompt "Property Mismatch" it means that the _Property Registry Number_ supplied is already registered to some other SSN or individual.
        * Both the above errors are not treated as failure so ethers will be charged as for successful transactions.
4. Viewing the registered _Property Registry Number_ with owner's _SSN_
      * Only the admin can view the registered properties and their owner
        * The first account in Ganache/test-rpc will be the owner under unchanged configurations
      * The owner needs to refresh the page after logging into her account with Metamask to see the registered properties.


## Blockchain Technologies utilized:

1. MultiChain: https://github.com/seetadev/ethopsud/tree/main/PropTech-Modules/BNB-smart-contract-light-client

2. BNB: https://github.com/seetadev/ethopsud/tree/main/PropTech-Modules/BNB-smart-contract-light-client

3. Polygon

4. Fantom


## UD Login for Ethops Minter (EthOps NFT Minter and the feature integration of "Login With Unstoppable")
Steps to setup and run the app:
1. Clone the repo and make sure you are in the project directory
2. Install dependencies with `yarn install`
3. Update `.env.example` file with your Unstoppable Domains keys
4. Run `yarn start` to start the local server at http://localhost:3000/ 

