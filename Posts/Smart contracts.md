
Goal: Make a web application using smart contracts. The use case was event invitations where the user confirms their presence and leave a message to be registered on the blokchain. I used heavily the technologies used in the course https://build.w3d.community/courses/Solidity_And_Smart_Contracts

Link for the application:

Link for github: https://github.com/CristianeMaragno/smart-contract-app and https://github.com/CristianeMaragno/smart-contract-frontend

For starters, what is the block chain and what are smart contracts?

The blockchain can be seen as a decentralized database where the data is stored as
blocks linked together in a chain. Is called decentralized because it doesn't exist in one server, but with copies in multiple unrelated machines and changes are only accepted with the consent of most part of the network. Is a very useful way of having transactions without the need for a trusted middle man, there is less risk of the data being lost because of the amount of copies and more security because difficulty of violation.
You can read more about it in this article(https://towardsdatascience.com/a-deep-dive-into-blockchain-d1eb753fb74c)

Smart contracts are  programs stored on a blockchain that run when predetermined conditions are met. Cannot be changed and bring all the the benefits of the blockchain: Security, transparency and speed of automation. An example of a simple smart contract using the programming language Solidity:

```
contract InvitationPortal {
	uint256 totalConfirmations;
	
	event NewConfirmation(address indexed from, uint256 timestamp, string message);
	
	struct Confirmation {
		address guest; // Endereço do usuário que deu tchauzinho
		string message;
		uint256 timestamp;
	}
	
	Confirmation[] confirmations;
	
	constructor() {
		console.log("Wow, i'm a smart contract");
	}
	
	function confirm(string memory _message) public {
		totalConfirmations += 1;
		console.log("%s confirmed presence! With message %s", msg.sender, _message);
		
		confirmations.push(Confirmation(msg.sender, _message, block.timestamp));
		emit NewConfirmation(msg.sender, block.timestamp, _message);
	}
	
	function getTotalConfirmations() public view returns (uint256) {
		console.log("We have a total of %d confirmations!", totalConfirmations);
		return totalConfirmations;
	}
}
```

Ok, but how to make all this really work? Let's know of the elements and tools needed

**Solidity**

Solidity is a high level programming language created in 2014 by one the founders of the blockchain Ethereum and is used to create smart contracts. There are other alternatives, but solidity is the most widely used in the moment.

**Environment**

A great challenge is how to develop locally, for this the Hardhat Ethereum development environment was very convenient because it can
- Create a fake local Ethereum blockcain;
- Create fake wallets and currency for testing;
- Help make the debugging a lot easier.

**Deployment**

Alchemy is web3 development platform with a generous free tier plan and many products and tools. In a blockchain all interactions are transactions, including the deploy, and the platform makes easy for us to implant our smart contract in the chosen blockchain.

Is important to remember that a smart contract can't be changed, what means that every time you make a change, you have to repeat de the deploy process
1. Deploy again using Alchemy;
2. Save address of our contract on the blockchain;
3. Update were the smart contract is being called, because you created a completely new one.

When using a public blockchain, there's complete transparency and you can track your transaction using sites like https://sepolia.etherscan.io/

**Using smart contracts**

After the deploy, our smart contract is already living in the block chain, but how can we access and use it?
An example of utilization is building a website and give it information about contract, like address in block chain, functions available, etc. When the user access our website and connect their Metamask wallet, is then possible access the blockchain, find and execute our smart contract.

Our contract files -> Alchemy -> Blockchain

Blockchain -> Metamask wallet -> Our website

**Other important questions**

- What is the Ethereum Virtual Machine (EVM)? https://ethereum.org/en/developers/docs/evm/
- What is the Etherium network and why there are multiple? https://ethereum.org/en/developers/docs/networks/#:~:text=Ethereum%20networks%20are%20groups%20of,for%20testing%20and%20development%20purposes.
- What is gas? https://ethereum.org/en/developers/docs/gas/
- How to test with fake money? https://sepoliafaucet.com/

**Conclusion**

Blockchain and Smart contracts are  interesting technologies that can change many of our current paradigms dealing with money, business deals and numerous other applications where they are starting to be used and even areas we can't imagine right now. 
Is completely worth it to be aware and learning about these tools and concepts that definitely came to stay.