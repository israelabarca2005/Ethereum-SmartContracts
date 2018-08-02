# Ethereum-SmartContracts
Smart Contract Course


This project will touch the bases on Smart Contracts. We are going to create a smart contract using Solidity, set up a local environment to deploy and consume the smart contract. Using Truffle to set up the environment and Ganche to simulate a local blockchain where the contract will be deployed. The following topics will be covered:

1. Installation of NodeJS
2. Setting up Truffle and Ganache
3. Truffle Environment Overview and Settings
4. Solidity Principles
5. Smart Contract Compilation and Deployment
6. Interacting with Ethereum network via WEB3 API 
7. Executing a Smart Contract

Note: We will use windows 10 OS, however is very similar on Linux or MAC OS


Installing NodeJS

Download NodeJS according to the OS you are using, in this case the Windows Installer. 

Link: https://nodejs.org/en/download/

Once nodeJS is downloaded we can verify the version installed along with NPM.

Type the following command on a windows command line:
> “node –-version”
* v8.9.0
> “npm --version”
* 5.5.1
The output should return the version installed in your computer, in case you don’t see the version make sure you install the right version, refer to the link above.


Setting up Truffle and Ganache

Now that we have installed NodeJs we are going to install Truffle and Ganache:

Type the following command on a windows command line:
> npm install -g truffle
* C:\Users\User Name\AppData\Roaming\npm

The output will be a path to the installation dir, but we want to be position at the npm directory to verify the version of truffle.



Type the following command on a windows command line:
> Truffle version
* Truffle v4.1.13 (core: 4.1.13)
* Solidity v0.4.24 (solc-js)

We now see Truffle version and additionally we are shown the solidity version as well.
Now it´s time to install Ganache!

We have the option to install the graphical version, but we are going to work with the command-line version formerly known as TestRPC. 

Type the following command on a windows command line:
> npm install -g ganache-cli

The output should be the version installed and the path to the installation folder (Should be same as Truffle).



If you want to try out the GUI version download here: https://github.com/trufflesuite/ganache/releases



Truffle Environment overview and settings

Up to this point we have done all the installations needed on our computer to compile and deploy our smart contract. Now we are going initialize our truffle environment where our smart contract will be placed.
Before getting started we are going to back up for a sec. Let’s set up our environment variables so we execute our commands from any directory. 

Go to your environment variable options:
> Click Environment Variable button
> Under user variables select “Path” a new options window will pop-up
> Click add and place the path where truffle and ganache were installed, in our case: C:\Users\User Name\AppData\Roaming\npm

Once this is done, we can now set up our truffle environment. Create a new directory where you want to set up your environment, in my case I created a directory as follows: 
> C:\Blockchain\Truffle_Env
No in the command-line I will place myself inside this new directory.


Type the following command on a windows command-line:
> Truffle init
The following directories and files were created:

Contracts: This is the directory for our Solidity contracts.
Migrations: This is the directory for the scriptable deployment files.
test: This is the directory for test files for testing your contracts and apps.
truffle: This is the truffle configuration file.
truffle-config: This is also the truffle configuration file however, you may encounter problems when executing a truffle command since windows first tries to find executable files. One way to solve this is to use this configuration file instead or change truffle.cmd in our installation folder to truff.cmd, if you take the second approach the commands will change to truff not truffle. In our case we are just going to use this configuration file and delete truffle.js.

Now we are going to configure our truffle-config.js file. 

It should look something like this:

module.exports = {
  networks: {
    ganache: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*"
    }
  }
};

As you can see we have set up our file pointing to our Ethereum Client Ganache which will listen on localhost (127.0.0.1) port 8545.

Our environment and settings are now ready. Its time to learn about solidity and program our first smart contract.


Solidity Principles

We are going to cover the basics of Solidity, for further research please visit the documentation available at:

http://solidity.readthedocs.io/en/v0.4.24/solidity-in-depth.html

Solidity is a contract-oriented, high-level language for implementing smart contracts. It was influenced by C++, Python and JavaScript and is designed to target the Ethereum Virtual Machine (EVM).

Solidity is statically typed, supports inheritance, libraries and complex user-defined types among other features.

The following code is an example of a very basic solidity contract, a value is being store and nothing else.


pragma solidity ^0.4.0;

contract SimpleStorage {
    uint storedData;

    function set(uint x) public {
        storedData = x;
    }

    function get() public view returns (uint) {
        return storedData;
    }
}

This example is from the Solidity documentation web site that was mention earlier. 
The first line of code simply tells source code language and version. In general, pragmas are instructions for the compiler about how to treat the source code. The sign (^) before the 0.4.0 explicitly tells the compiler it will only take versions from 0.4.0 or above. This is to avoid using a version that is not secure or a deprecated version. 

pragma solidity ^0.4.0;

In the next line the contract is declared. The word contract followed by the name of that contract and everything that is inside the brackets will be part of the contract. In this case, the contract name will be SimpleStorage. Contract has similarities to Class in other languages such as inheritance, class variables, access modifiers etc.

contract SimpleStorage {

Class variables are those that are declared outside a function. We can declare a variable public or private. Private can’t directly query data, and public makes externally readable by users or contracts. The variable declared in this contract is an unsigned integer public by default.


uint storedData;


We can declare types of functions, in this case we have what is called setter, there we can implement setters and getter in Solidity. The word function defines a function followed by the name, inside the parenthesis we define the types and variables it takes in as parameters and finally we define the access modifier, in this case is declared as public. Inside our set function we have a variable set to the value of X which is the parameter we received.


function set(uint x) public {
        storedData = x;
    }

The last part of the code is very similar to the one above, except for a view and a variable being returned. The view word means that the function will not alter the storage state in any way. In previous versions of Solidity, the word “constant” was used instead. The word pure could also be used and it would indicate that the function could not even read that storage state it’s way more restrictive.


    function get() public view returns (uint) {
        return storedData;
    }
}

As it was mention before the syntax is very similar to what we know today as JavaScript and Python, if you have used any of these languages or another OOP language it should look very familiar to you.



Smart Contract Compilation and Deployment

Now that we have everything set up it’s time to compile and deploy. For this example, we are going to program a simple contract printing out a string “Hello World”. To do this we are going to follow the next steps:

1. Open the directory where we set up the environment (C:\Blockchain\Truffle_Env) where we executed truffle init.
2. Once in this directory we are going to place our smart contract inside the “contracts” folder.
3. This project which you can download has the structure and also contract already added to the “contracts” folder. All you need to do is compile and deploy.
4. To compile open a command-line and set the position where we have our environment and type the following command:
* truffle compile
The output should be something like:

C:\Blockchain\Truffle_Env>truffle compile
Compiling .\contracts\Greeter.sol...
Writing artifacts to .\build\contracts


You may encounter compilation problems, work around them. The most common can be a compilation error or warning on the syntax. Just make sure you are using the right version specified on your contract. For example, if you are using the word function to declare a constructor, when you use a recent solidity version the correct way to do it is to just place a method inside the contract with the word “constructor” instead of “function”.


Before


     function nameofcontract() { owner = msg.sender; }


After

	constructor(bytes32 _name) public {}


So, just watch out on what version you are compiling on.


The last line on the output from our compiling command, is telling it wrote something on that directory, which happens to be our compiled contracts. Congrats, you have compiled your contract!

The compiled contracts are in the folder .\build\contracts, we are not going to touch on that on this time, that will be for another time. All we must know that this directory is where our contracts will be put in after being compiled therefore, a lot of information can be bound here. If your contract It’s inside this directory it means you are in the right path.

 It’s time to get our contract deployed so let’s get on that. So, what do we have to do to get it on our simulated blockchain, can someone guess? Well, the first thing is obviously to get our blockchain up and running. To do that, we are going to type the following command on a new command-line:

ganache-cli

You should get 10 accounts about 100eth each and its respective private keys. At this point, we assume you are familiar with the concepts of accounts, private keys, ether, wallets, etc. But what about Gas Price and Gas Limit. As we know, to be able to write into the Ethereum blockchain we must pay a transaction fee, this fee is what we call Gas which is a unit of measure for computational power. The gas price is how much eth we are willing to pay for each gas unit. The gas limit is how much gas we are willing to spend for a specific transaction.  

Now that we know the very basics of gas and how we can use it to get our transactions into the blockchain, let’s see this in real life. After executing the previous command our client should be up and running on localhost port 8545. Ganache automatically will set our Gas Price and Gas Limit. When deploying to a real net set these values wisely and remember that if you don´t give enough gas to a transaction, it can end up not executing correctly meaning it will be drop along the way. With that said, we should have at least two command-line windows open. The first is where our environment is located and the second is our ganache client running on port 8545.

We are ready to deploy our contract into our local blockchain, we are going to do this with an API from JavaScript named Web3. This API will let us interact with our environment. To do this, run the following command in your root directory from our environment. 


C:\Blockchain\Truffle_Env>truffle console --network ganache


This command should provide a console. We are now inside and can interact with the blockchain. Notice, in the other command-line windows we should get some output of what we are doing in our blockchain. To deploy our contract we need two things:

1. An Account
2. Gas (Ether)

Ganache already provided us with the two. Type the command in the truffle command-line:


truffle(ganache)> web3.personal.listAccounts


This command will give us a list of Addresses available, in the main net or test net we will have to set our account to be able to deploy the contract. Ganache will do this automatically for us. So finally, lets deploy the contract by typing the following commands on the truffle command-line:


truffle(ganache)> web3.eth.accounts[0]

This command shows the owner of the contract, meaning it will use this account to deploy. Now lets type the following command:


truffle(ganache)> Greeter.new("Hello World From Ganache!")


This command will put our contract up in the blockchain, if you open up the contract Greeter.sol, you will notice that this contract inherits from Mortal which sets the owner of the contract in the constructor and also receives a string value in the constructor of the Greeter contract.
There should be a lot of information displayed after executing the command, lets focus on the most important ones. 

1. Transaction Hash
2. Address
3. From

 The transaction hash is the resulting hash from the transaction details we performed. The address is where our contract has been deployed, so in order to call our smart contract we have to know the address where its located. The From is going to tell who deployed the contract, basically is indicating which account is the owner of the contract that was deployed.



