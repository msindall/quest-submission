# quest-submission
## Emerald City Cadence Bootcamp

### Chapter 1
#### Day 1

Explain what the Blockchain is in your own words.
  - A Blockchain is a Shared Database. It should be decentralized in a manner that the database is spread across multiple locations. This prevents a single point of failure and is one of the main reasons a blockchain is so secure. It should be public in the sense that anyone, anywhere can view the data in the database at any time. This transparency reduces the likelihood of hiding things in the database. It should also be Open in the sense that anyone can interact with the blockchain and create content.

Explain what a Smart Contract is. You can read this to help you, but you don't have to: https://www.ibm.com/topics/smart-contracts
 - A smart contract is a program with a way of defining a ruleset to store or use information in a desired manner, and then execute and store that information onto a blockchain. It is an agreement between the creator and signer to perform certain actions. Due to a blockchain being open and usable for anything, a smart contract is a way of telling it what to do or information to store, how to do it, and with who. They are fulfilled when requirements are met without the need for a middleman to ease and speed up the process of completion.

Explain the difference between a script and a transaction.
- A script is a way of viewing data on the blockchain and can be run by anyone at any time and does not cost money. This allows us to read information in the blockchain and is part of the structure that makes a blockchain Public and accessible.
- A transaction will modify, add or remove data in the blockchain, and thus will cost money and usually need to be verified by other means on the blockchain in order to be successful.


#### Day 2
What are the 5 Cadence Programming Language Pillars?
- Safety and Security
- Clarity
- Approachability
- Developer Experience
- Resource Oriented Programming


In your opinion, even without knowing anything about the Blockchain or coding, why could the 5 Pillars be useful (you don't have to answer this for #5)?
1. Safety and Security is the key to onboarding the masses. No one wants to invest to lose money. Losing money can come in the form of a hack, poorly designed code or interfaces, or general misunderstanding of what the user is doing. Focusing on the user's safety and security first means more users will want to use it.
2. Clarity in anything is important. The better instructions we have, the better we can execute. If we can communicate clearly, everything goes exponentially quicker. Best illustrated by the kid's game Telephone tag, if one person isn't clear on the instructions, it quickly goes wrong.
3. Approachability is important to attract developers to build the ecosystem. If I can write this code without having coded for years, it should be easier for me to also get good at it, and the quicker we all master the code the quicker it grows in utility.
4. If the developer experience is poor, or the onboarding is too extensive, I wouldn't even try to learn it. Having easy to use tools is important, especially in attracting new developers to the ecosystem and then keeping them.
5. File sizes, lost data, and careless programming could all be reduced by having to actually use the resources you create. Much like wasting food or fuel, the more we limit it the better hte habits we have.



### Chapter 2
#### Day 1

```cadence
pub contract JacobTucker {

    pub let is : String

    init() {
        self.is = "the best!"
    }
}
```

```cadence
import JacobTucker from 0x03

pub fun main(): String {
    return JacobTucker.is
}
```

![JacobIsTheBest](https://user-images.githubusercontent.com/5509347/172382895-67c1dfb1-e0f0-4f44-b958-bf86e0b5bd28.PNG)


#### Day 2

Explain why we wouldn't call changeGreeting in a script.
- Scripts are only meant to view data and do not cost gas fees. Changing data on the blockchain is only meant to happen in a transaction which costs gas fees. Scripts are also public and require no signer meaning anyone could change the greeting.

What does the AuthAccount mean in the prepare phase of the transaction?
- The AuthAccount is the signer of the transaction and contains information about the address's account

What is the difference between the prepare phase and the execute phase in the transaction?
- The prepare phase has access to the AuthAccount whereas the Execute phase does not. In theory, all work could be done in the prepare phase, but it is more readable and secure to use the execute phase to do the work once you have prepared only the necessary information in the prepare phase

Add two new things inside your contract:
A variable named myNumber that has type Int (set it to 0 when the contract is deployed)
A function named updateMyNumber that takes in a new number named newNumber as a parameter that has type Int and updates myNumber to be newNumber
```cadence
pub contract HelloWorld {

    pub var greeting: String
    pub var myNumber : Int

    init() {
        self.greeting = "Hello, World!"
        self.myNumber = 0
    }

    pub fun changeGreeting(newGreeting: String) {
        self.greeting = newGreeting
    }

    pub fun updateMyNumber(newNumber : Int) {
        self.myNumber = newNumber
    }
}
```


Add a script that reads myNumber from the contract
```cadence
import HelloWorld from 0x01

pub fun main(): String {
    log(HelloWorld.greeting)
    log(HelloWorld.myNumber)

    return HelloWorld.greeting
}
```

Add a transaction that takes in a parameter named myNewNumber and passes it into the updateMyNumber function. Verify that your number changed by running the script again.

```cadence
import HelloWorld from 0x01

transaction(myNewGreeting: String, myNewNumber: Int) {

  prepare(signer: AuthAccount) {}

  execute {
    HelloWorld.changeGreeting(newGreeting: myNewGreeting)
    HelloWorld.updateMyNumber(newNumber: myNewNumber)
  }
}
```
