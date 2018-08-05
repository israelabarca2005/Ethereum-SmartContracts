## Smart Contract Course


This mini-course will touch the bases on Smart Contracts. We are going to create a smart contract using Solidity, set up a local environment to deploy and execute the smart contract’s functionality. We will work with Truffle to set up the environment and Ganche to simulate a local blockchain where the contract will be deployed. The following topics will be covered:

1. Installation of NodeJS
2. Setting up Truffle and Ganache
3. Truffle Environment Overview and Settings
4. Solidity Principles
5. Smart Contract Compilation and Deployment
6. Interacting with Ethereum network via WEB3 API  

Note: Windows 10 is the OS we are going to use.


# Installing NodeJS

Download NodeJS according to the OS you are using, in this case the Windows Installer. 

	Link: https://nodejs.org/en/download/

Once nodeJS is downloaded we can verify the version installed along with NPM.

Type the following command on a windows command line:

>node –-version
	v8.9.0

>npm --version
	V5.5.1

The output should return the version installed in your computer. If the version is not shown in the command-line windows, then the installation went wrong. Go back and reinstall.


# Setting up Truffle and Ganache

Now that we have installed NodeJS we are going to install Truffle and Ganache.
Type the following command on a windows command-line:

>npm install -g truffle
	C:\Users\User Name\AppData\Roaming\npm

The output will be a path to the installation directory and we can verify the version, but we have set the path to the previous output to successfully verify the version of truffle.
Type the following command on a windows command-line:

>C:\Users\User Name\AppData\Roaming\npm>Truffle version

	Truffle v4.1.13 (core: 4.1.13)
	Solidity v0.4.24 (solc-js)

We now see Truffle version and additionally we are shown solidity compiler version as well, it was also installed along with Truffle.

Now it’s time to install Ganache Client!
We have the option to install the graphical version, but we are going to work with the command-line version formerly known as TestRPC.
Type the following command on a windows command line:

>npm install -g ganache-cli

The output should be the version installed and the path to the installation folder (Should be same as Truffle).
If you want to try out the GUI version download here: 

	https://github.com/trufflesuite/ganache/releases


# Truffle Environment overview and settings

Up to this point we have done all the installations needed on our computer to compile and deploy our smart contract. Now we are going initialize our truffle environment where our smart contract will be placed.

Before getting started we are going to back up for a sec. Let’s set up our environment variables so we can execute our commands from any directory. 

Go to your environment variable options:

	Click Environment Variable button
	Under user variables select “Path” a new options window will pop-up
	Click add and place the path where truffle and ganache were installed, in our case: C:\Users\User Name\AppData\Roaming\npm

Once this is done, we can now set up our truffle environment. Create a new directory where you want to set up your environment, in my case I created a directory as follows: 

>C:\Blockchain\Truffle_Env

In the command-line I will place myself inside this new directory.

Type the following command on a windows command-line:

>Truffle init

The following directories and files were created:

	Contracts: This is the directory for our Solidity contracts.

	Migrations: This is the directory for the scriptable deployment files.

	Test: This is the directory for testing files and contracts.

	truffle: This is the truffle configuration file.

	truffle-config: This is also the truffle configuration file however, you may encounter problems when executing a truffle 				command since windows first tries to find executable files.

One way to solve this is to use this configuration file instead or change truffle.cmd in our installation folder to truff.cmd, if you take the second approach the commands will change to truff not truffle. In our case we are just going to use this configuration file and delete truffle.js.

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
Our environment and settings are now ready. It’s time to learn about solidity and code our first smart contract.


# Solidity Principles

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

>pragma solidity ^0.4.0;

The first line of code simply tells source code language and version. In general, pragmas are instructions for the compiler about how to treat the source code. The sign (^) before the 0.4.0 explicitly tells the compiler it will only take versions from 0.4.0 or above. This is to avoid using a version that is not secure or a deprecated version. 

>contract SimpleStorage {

In the next line the contract is declared. The word contract followed by the name of that contract and everything that is inside the curly brackets will be part of the contract. In this case, the contract name will be SimpleStorage. Contract has similarities to Class in other languages such as inheritance, class variables, access modifiers etc.

>uint storedData;

Class variables are those that are declared outside a function. We can declare a variable public or private. Private can’t directly query data, and public makes externally readable by users or contracts. The variable declared in this contract is an unsigned integer public by default.

>function set(uint x) public {
>        storedData = x;
>    }

We can declare functions, in this case we have what is called setter, we can implement setters and getter in Solidity. The word function defines a function followed by the name, inside the parenthesis we define the types and variables it takes in as parameters and finally we define the access modifier, in this case it’s declared as public. Inside our set function we have the variable storedData set to the value of X which is the parameter we received.

>function get() public view returns (uint) {
>       return storedData;
>    }
>}

The last part of the code is very similar to the one above, except for a view and a variable being returned. The view word means that the function will not alter the storage state in any way. In previous versions of Solidity, the word constant was used instead. The word pure could also be used and it would indicate that the function could not even read that storage state it’s way more restrictive.

As it was mention before the syntax is very similar to what we know today as JavaScript and Python, if you have used any of these languages or another OOP language it should look very familiar to you.


# Smart Contract Compilation and Deployment

Now that we have everything set up it’s time to compile and deploy. For this example, we are going to code a simple contract printing out a string “Hello World”. To do this we are going to follow the next steps:

1. Open the directory where we set up the environment
   (C:\Blockchain\Truffle_Env) we executed truffle init command earlier.

2. Once in this directory we are going to place our smart contract inside the “contracts” folder.

3. This project which you can download here has the correct structure and the contract already added to the “contracts” folder. All you need to do is compile and deploy.

4. To compile open a command-line and set the position where we have our environment and type the following command:

>C:\Blockchain\Truffle_Env>truffle compile

The output should be something like:

	Compiling .\contracts\Greeter.sol...
	Compiling .\contracts\Migrations.sol...
	Writing artifacts to .\build\contracts

You may encounter compilation problems, work around them. The most common can be a compilation error or warning on the syntax. Just make sure you are using the right version specified on your contract. For example, if you are using the word function to declare a constructor, when you use a recent solidity version the correct way to do it is to just place a method inside the contract with the word “constructor” instead of “function”.

Before

     function nameofcontract() { owner = msg.sender; }

After

	constructor(bytes32 _name) public {}

So, just watch out on what version you are compiling on.

The last line on the output from our compiling command, is telling it wrote something on that directory, which happens to be our compiled contracts. Congrats, you have compiled your contract!

The compiled contracts are in the folder .\build\contracts, we are not going to touch on that this time, that will be for another time. All we must know is that this directory is where our contracts will be put in after being compiled therefore, a lot of information can be bound here. If your contract is inside this directory it means you are in the right path.

It’s time to get our contract deployed so let’s get on that. Well, the first thing is obviously to get our blockchain up and running. To do that, we are going to type the following command on a new command-line:

>ganache-cli

You should get 10 accounts about 100eth each and its respective private keys. At this point, we assume you are familiar with the concepts of accounts, private keys, ether, wallets, etc. But what about Gas Price and Gas Limit. As we know, to be able to write into the Ethereum blockchain we must pay a transaction fee, this fee is what we call Gas which is a unit of measure for computational power. The gas price is how much eth we are willing to pay for each gas unit. The gas limit is how much gas we are willing to spend for a specific transaction.  

Now that we know the very basics of gas and how we can use it to get our transactions into the blockchain, let’s see this in real life. After executing the previous command our client should be up and running on localhost port 8545. Ganache automatically will set our Gas Price and Gas Limit. When deploying to a main net set these values wisely and remember that if you don´t give enough gas to a transaction, it can end up not executing correctly meaning it will be drop along the way. With that said, we should have at least two command-line windows open. The first is where our environment is located and the second is our ganache client running on port 8545.

We are ready to deploy our contract into our local blockchain, Truffle will make it a bit easier since we don’t have to use Migrations where we would have to set up a few more things and run a different migration command. Instead, we are going to do this by interacting directly with our blockchain. To do this, run the following command in your environment directory:

>C:\Blockchain\Truffle_Env>truffle console --network ganache

This command should provide a console. We are now inside and can interact with the blockchain. Notice, in the other command-line windows we should get some output from the commands executed in the blockchain. To deploy our contract, we need two things:

	1. An Account
	2. Gas (Ether)

Ganache already provided us with the two. Type the following command in the truffle command-line:

>truffle(ganache)> web3.personal.listAccounts

This command will give us a list of Addresses available, in the main net or test net we will have to set our account to be able to deploy the contract through migration. Ganache and Truffle will do this automatically for us. So finally, lets deploy the contract by typing the following commands on the truffle command-line:

>truffle(ganache)> web3.eth.accounts[0]

This command shows the owner of the contract, meaning it will use this account to deploy. Now type the following command:

>truffle(ganache)> Greeter.new("Hello World From Ganache!")

This instruction will put our contract up in the blockchain, if you open the contract Greeter.sol, you will notice that this contract inherits from Mortal which sets the owner of the contract in the constructor method, so we have two embedded contracts in one .sol file. The Greeter contract receives a string value in the constructor and sets the value to a variable.

There should be a lot of information displayed after executing the command, lets focus on the three most important. 

	1. Transaction Hash
	2. Address
	3. From

The transaction hash is the resulting hash from the transaction done when we deployed the contract. The address is where our contract has been deployed, therefore to execute the smart contract we must know the address where it is located. The from is the information of the account who deployed the contract, basically indicates the owner of the contract.


# Interacting with Ethereum Network Via Web3 Api

As you saw earlier we were able get some information using the Api web3. This API is a set of libraries exposing different modules which allow you to interact with an Ethereum node locally or remotely using HTTP or IPC connection.

While still on the console we can make use of the Api to interact with the blockchain, now let’s execute the function exposed by the contract we deployed, if you recall our contract Greeter has a function greet that returns a string, this string value was set to “Hello World From Ganache!” in the contract we deployed since the constructor set this value to the variable greeting.

Now let’s call the function greet and we can do this since we declared it public. Type the following command:

>truffle(ganache)> Greeter.at("0x3699a1e9b9811d48c26d511a8e802a3f39fc4088").greet()

The address placed inside the at method is the address of the contract we deployed earlier, so make sure you change it with the address of your own contract. 

Once you execute the command, you should see the message “Hello World from Ganache!” in the command-line.
Now it’s time to experiment with web3, type the following command:

>truffle(ganache)>web3

As you can see the output is a whole list of methods and modules available. Some are to display information of your account, set gas price, gas limit and many other things.

You can do some interesting stuff with web3 api, we are not going to go too much in depth in this article, but I will leave a reference where you can view valuable information. The link below will take you to the documentation where you can start experimenting with all the functionality available.

	https://web3js.readthedocs.io/en/1.0/


# Conclusion

We were able to set up an environment and run a local blockchain through Truffle and Ganache. We also went over the basics of Solidity reviewing a smart contract anatomy, we compiled and deployed a contract on our Ethereum Ganache client node. With the Web3 Api we interacted with the blockchain, using commands like truffle console we also consumed the contract we deployed and executed a public method. As you can see it’s quite easy to implement a smart contract and test it with these tools available. Instead of having to synchronize a full node with a test net or a main net this can be a quick way to set yourself up and experiment with the blockchain ecosystem before going to the real deal.
