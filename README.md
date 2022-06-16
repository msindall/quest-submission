# quest-submission
## Emerald City Cadence Bootcamp

### Chapter 1
### Day 1

Explain what the Blockchain is in your own words.
  - A Blockchain is a Shared Database. It should be decentralized in a manner that the database is spread across multiple locations. This prevents a single point of failure and is one of the main reasons a blockchain is so secure. It should be public in the sense that anyone, anywhere can view the data in the database at any time. This transparency reduces the likelihood of hiding things in the database. It should also be Open in the sense that anyone can interact with the blockchain and create content.

Explain what a Smart Contract is. You can read this to help you, but you don't have to: https://www.ibm.com/topics/smart-contracts
 - A smart contract is a program with a way of defining a ruleset to store or use information in a desired manner, and then execute and store that information onto a blockchain. It is an agreement between the creator and signer to perform certain actions. Due to a blockchain being open and usable for anything, a smart contract is a way of telling it what to do or information to store, how to do it, and with who. They are fulfilled when requirements are met without the need for a middleman to ease and speed up the process of completion.

Explain the difference between a script and a transaction.
- A script is a way of viewing data on the blockchain and can be run by anyone at any time and does not cost money. This allows us to read information in the blockchain and is part of the structure that makes a blockchain Public and accessible.
- A transaction will modify, add or remove data in the blockchain, and thus will cost money and usually need to be verified by other means on the blockchain in order to be successful.

-----------------------------------------------------------------------------------------------------------------------------


### Day 2
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


-----------------------------------------------------------------------------------------------------------------------------



### Chapter 2
### Day 1

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


-----------------------------------------------------------------------------------------------------------------------------


### Day 2

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

![image](https://user-images.githubusercontent.com/5509347/172389191-3739e456-443f-4b90-8154-edf6c2a4ac03.png)


-----------------------------------------------------------------------------------------------------------------------------


### Day 3

In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.
```cadence
pub fun main() {
    var favPpl: [String] = ["Jacob Tucker", "Chuck Norris", "Batman"]
    log(favPpl)
}
```

In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!
```cadence
pub fun main() {
    var socialMedias: {String: UInt64} = {"Facebook": 3, "Instagram": 4, "Twitter": 1, "YouTube": 2, "Reddit": 5, "LinkedIn" : 6}
    log(socialMedias)
}
```
Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).
 - Dictionaries return an optional value, meaning it could be a nil value. The force unwrap tells the code to error if the value is nil instead of the type it expects. In the social media example above, if we tried to read the number value for "TikTok" it would return nil because the dictionary entry does not exist, and the force unwrap operator is needed to error the program

Using this picture below, explain...

What the error message means
 - We are wanting to return a String, but actually returning an Optional String 
Why we're getting this error
- due to dictionaries returning optionals when accessed. This is because the entry you are looking for may not exist.
How to fix it
- Ideally, return the optional "String?" and let the accessor handle any errors. Alternatively, use the Force Unwrap "thing[0x03]!" operator in the return statement to error when nil



-----------------------------------------------------------------------------------------------------------------------------


### Day 4

Deploy a new contract that has a Struct of your choosing inside of it (must be different than Profile).
Create a dictionary or array that contains the Struct you defined.
Create a function to add to that array/dictionary.

```cadence
pub contract BeerStruct {

    pub var breweryListings :{String : Beer }

    pub struct Beer {
        pub var name: String
        pub var style: String
        pub var abv : UFix64
        pub var ibu : UFix64

        init(_beerName: String, _style: String, _abv : UFix64, _ibu : UFix64){
            self.name = _beerName
            self.style = _style
            self.abv = _abv
            self.ibu = _ibu
        }
    }

    init() {
        self.breweryListings = {}
    }

    pub fun addListing(_breweryName: String, _beerName: String, _style: String, _abv : UFix64, _ibu : UFix64){
        var newBeer = Beer(_beerName: _beerName, _style: _style, _abv: _abv, _ibu: _ibu)
        self.breweryListings.insert(key: _breweryName, newBeer)
    }
}
```

Add a transaction to call that function in step 3.
```cadence
import BeerStruct from 0x01

transaction(_breweryName: String, _beerName: String, _style: String, _abv : UFix64, _ibu : UFix64) {
  prepare(signer: AuthAccount) {}

  execute {
    BeerStruct.addListing(_breweryName: _breweryName, _beerName: _beerName, _style: _style, _abv: _abv, _ibu: _ibu)
  }
}
```
![image](https://user-images.githubusercontent.com/5509347/172452316-3462437a-79da-477a-a70e-0ce1bc319111.png)


Add a script to read the Struct you defined.
```cadence
import BeerStruct from 0x01

pub fun main() {
    log(BeerStruct.breweryListings)
}
```
![image](https://user-images.githubusercontent.com/5509347/172452537-747703de-aed5-4e83-908a-9c8eb9e4e7e3.png)



-----------------------------------------------------------------------------------------------------------------------------

### Chapter 3
### Day 1



In words, list 3 reasons why structs are different from resources.
- Only 1 version of a resource can ever exist
- Resources must be specially created and destroyed
- resources must be "moved" between locations and cannot be lost

Describe a situation where a resource might be better to use than a struct.
- NFT's are the perfect use case of a resource that should only exist once, shouldn't be copied, cannot be lost and must be handled with care
- security permissions could be another great use case where you can only access something as long as you have a security resource. if you lose credentials to that resource you must regain access, or they can be transfered to another person but the permissions cannot be lost or copied.

What is the keyword to make a new resource?
- create

Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?
- No. the create keyword can only be used inside the contract level, so if there is no public function to create a resource, then you will not be able to.

What is the type of the resource below?
- it is a Jacob type resource.

Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.

FIXED:
```cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { // there is 0 here
        let myJacob <- create Jacob() // there are 0 here
        return <- myJacob // there is 0 here
    }
}
```



-----------------------------------------------------------------------------------------------------------------------------


### Day 2

```cadence
pub contract BeerResource {

    pub var breweryDictionary :@{String : Beer } //dictionary
    pub var beerArray : @[Beer]  //array

    pub resource Beer {
        pub var breweryName: String
        pub var name: String
        pub var style: String
        pub var abv : UFix64
        pub var ibu : UFix64

        init(_breweryName: String, _beerName: String, _style: String, _abv : UFix64, _ibu : UFix64){
            self.breweryName = _breweryName
            self.name = _beerName
            self.style = _style
            self.abv = _abv
            self.ibu = _ibu
        }
    }

    init() {
        self.breweryDictionary <- {}
        self.beerArray <- []
    }

    //public create function
    pub fun createBeer(_breweryName: String, _beerName: String, _style: String, _abv : UFix64, _ibu : UFix64) : @Beer {
        return <- create Beer(_breweryName: _breweryName, _beerName: _beerName, _style: _style, _abv: _abv, _ibu: _ibu)
    }

    //ADDING
    pub fun addBeerToDict(_beer: @Beer) {
        let key = _beer.breweryName
        let oldBreweryListings <- self.breweryDictionary[key] <- _beer
        destroy oldBreweryListings
    }

    pub fun addBeerToArray(_beer: @Beer) {
        self.beerArray.append(<- _beer)
    }

    //REMOVING
    pub fun removeBeerFromDict(key: String) : @Beer {
        let beer <- self.breweryDictionary.remove(key: key) ?? panic("Could not remove Beer Resource")
        return <- beer
    }

    pub fun removeBeerFromArray(_index: Int) : @Beer {
        return <- self.beerArray.remove(at: _index)
    }
}
```



-----------------------------------------------------------------------------------------------------------------------------


### Day 3

Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.
- Used my example from previous day's resource work but added function:
```cadence
    //Get Reference
    pub fun getReference(key: String): &Beer {
        return &self.breweryDictionary[key] as &Beer
    }
```

Create a script that reads information from that resource using the reference from the function you defined in part 1.
```cadence
import BeerResource from 0x01

pub fun main(_breweryName: String) {
    let beerRef = BeerResource.getReference(key: _breweryName)
    log(beerRef.breweryName)
    log(beerRef.name)
    log(beerRef.style)
    log(beerRef.abv)
    log(beerRef.ibu)
}
```

Explain, in your own words, why references can be useful in Cadence.
- with resources being so important and secure, we will be using them a lot. They could hold large amounts of data we do not want to move around in memory a lot, which makes using references handy. If we are just reading information, there is no sense in moving that information anywhere in storage if we can read it from where it is.




-----------------------------------------------------------------------------------------------------------------------------


### Day 4


Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)
1. Restricting access to state information or functions - If a Beer resource has a Recipe associated with it, the brewer should be able to see it, but the graphic designer may not need to
2. Creating different rulesets for different applications using the same Resource - a Beer resource could be used by a Retailer or a Consumer and each may have different capabilities or information, but both could use the same physical Beer resource

Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.

```cadence
pub resource interface IBeer {
        pub var breweryName: String
        pub var name: String
        pub var retailPrice : UFix64
    }

    pub resource Beer : IBeer {
        pub var breweryName: String
        pub var wholesalePrice : UFix64
        pub var retailPrice : UFix64
        pub var name: String
        pub var style: String
        pub var abv : UFix64
        pub var ibu : UFix64

        init(_breweryName: String, _beerName: String, _style: String, _abv : UFix64, _ibu : UFix64){
            self.breweryName = _breweryName
            self.name = _beerName
            self.style = _style
            self.abv = _abv
            self.ibu = _ibu
            self.retailPrice = 0.0
            self.wholesalePrice = 0.0
        }
    }
```
![image](https://user-images.githubusercontent.com/5509347/172484604-15cfc038-7f79-4994-a681-f589021686ce.png)


How would we fix this code?

FIXED:
```cadence
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
      pub fun changeGreeting(newGreeting: String): String //added
    }

    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String //added

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Apple" //added
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!")
      log(newGreeting)
    }
}
```



-----------------------------------------------------------------------------------------------------------------------------


### Day 5

```cadence
access(all) contract SomeContract {
    pub var testStruct: SomeStruct

    pub struct SomeStruct {

        //
        // 4 Variables
        //

        pub(set) var a: String

        pub var b: String

        access(contract) var c: String

        access(self) var d: String

        //
        // 3 Functions
        //

        pub fun publicFunc() {}

        access(contract) fun contractFunc() {}

        access(self) fun privateFunc() {}


        pub fun structFunc() {
            /**************/
            /*** AREA 1 ***/
            /**************/
            //a : Write Scope - All Scope, Read Scope - All Scope
            //b : Write Scope - Current & Inner, Read Scope - All Scope
            //c : Write Scope - Current & Inner, Read Scope - Containing Contract
            //d : Write Scope - Current & Inner, Read Scope - Current & Inner

            //publicFunc : can be called, has ALL scope
            //contractFunc : can be called, within contract
            //privateFunc : can be called, is within itself
            self.publicFunc()
            self.contractFunc()
            self.privateFunc()
        }

        init() {
            self.a = "a"
            self.b = "b"
            self.c = "c"
            self.d = "d"
        }
    }

    pub resource SomeResource {
        pub var e: Int

        pub fun resourceFunc() {
            /**************/
            /*** AREA 2 ***/
            /**************/
            //a : Write Scope - All Scope, Read Scope - All Scope
            //b : Write Scope - Cannot write outside of Struct, Read Scope - All Scope
            //c : Write Scope - Cannot write outside of Struct, Read Scope - Containing Contract
            //d : Write Scope - Cannot write outside of Struct, Cannot read outside of Struct

            //publicFunc : can be called, has ALL scope
            //contractFunc : can be called, within contract
            //privateFunc : cannot be called, is not within struct
            let test = SomeStruct()
            test.publicFunc()
            test.contractFunc()
            //test.privateFunc() Error, function has private access
        }

        init() {
            self.e = 17
        }
    }

    pub fun createSomeResource(): @SomeResource {
        return <- create SomeResource()
    }

    pub fun questsAreFun() {
        /**************/
        /*** AREA 3 ****/
        /**************/
        //a : Write Scope - All Scope, Read Scope - All Scope
        //b : Write Scope - Cannot write outside of Struct, Read Scope - All Scope
        //c : Write Scope - Cannot write outside of Struct, Read Scope - Containing Contract
        //d : Write Scope - Cannot write outside of Struct, Cannot read outside of Struct

        //publicFunc : can be called, has ALL scope
        //contractFunc : can be called, within contract
        //privateFunc : cannot be called, is not within struct
        let test = SomeStruct()
        test.publicFunc()
        test.contractFunc()
        //test.privateFunc() Error, function has private access
    }

    init() {
        self.testStruct = SomeStruct()
    }
}


import SomeContract from 0x01

pub fun main() {
  /**************/
  /*** AREA 4 ***/
  /**************/
  //a : Write Scope - Should not write in a script, but technically can. Read Scope - All Scope
    //b : Write Scope - Cannot write outside of Struct, Read Scope - All Scope
    //c : Write Scope - Cannot write outside of Struct, Read Scope - cannot read outside of Containing Contract
    //d : Write Scope - Cannot write outside of Struct, Cannot read outside of Struct

    log(SomeContract.testStruct.a)
    log(SomeContract.testStruct.b)
    //log(SomeContract.testStruct.c)Error, field has contract access
    //log(SomeContract.testStruct.d)Error, field has private access
    SomeContract.testStruct.a = "Test"
    //SomeContract.testStruct.b = "Test" //error, cannot assign to b, field has public access, make settable
    //SomeContract.testStruct.c = "Test" //error, field has contract access
    //SomeContract.testStruct.d = "Test" //error, field has private access



    //publicFunc : can be called, has ALL scope
    SomeContract.testStruct.publicFunc()
    //SomeContract.testStruct.contractFunc() Error, function has contract access
    //SomeContract.testStruct.privateFunc() Error, function has private access
    SomeContract.testStruct.a = "a" //we shouldn't do this in a script
}
```



-----------------------------------------------------------------------------------------------------------------------------


### Chapter 4
### Day 1

Explain what lives inside of an account.
  - An account contains all contract code for that ccount (could be multiple contracts). In Flow, we are also allowed to have storage inside the account itself, instead of just inside the contracts. This means different contracts could access the same account storage.

What is the difference between the /storage/, /public/, and /private/ paths?
 - /storage can only be used by the account holder itself, and is the most private
 - /private can be used by anyone the account holder gives access to, restricting access to information to only those you want to know it
 - /public can be viewed by anybody. Do not put anything you don't want to share here.

What does .save() do? What does .load() do? What does .borrow() do?
 - .save will put data into the account storage where specified - like depositing money into a bank account
 - .load will take that saved data out of account storage - same as withdrawing money from a bank account
 - .borrow will allow you to read data from storage without taking it out. - like viewing your bank balance or account number, without touching your money

Explain why we couldn't save something to our account storage inside of a script.
 - Scripts do not have access to the AuthAccount since there is no signer of a transaction. We could get a public address and borrow details from it, but not save or load

Explain why I couldn't save something to your account.
 - /Storage is only accessible by the account itself for security reasons. I could allow you to view things in private or public storage, but no one but me would have access to directly manipulate my storage

Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:
```cadence

pub contract BeerContract {
    pub var testBeer : @Beer

    pub resource Beer {
        pub var name : String

        init() {
            self.name = "Spike's Corners IPA"
        }
    }

    pub fun createBeer(): @Beer {
        return <- create Beer()
    }

    init() {
        self.testBeer <- create Beer()
    }
}

```

A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.
```cadence
import BeerContract from 0x03

transaction() {

  prepare(signer: AuthAccount) {
    //create beer
    let testBeer <- BeerContract.createBeer()

    //save beer
    signer.save(<- testBeer, to: /storage/MyBeers)

    //load beer
    let newTestBeer <- signer.load<@BeerContract.Beer>(from: /storage/MyBeers) ?? panic("Could not load Beer Item")

    //log name of beer and destroy
    log(newTestBeer.name)
    destroy newTestBeer
  }

  execute {  }
}
```
A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
```cadence
import BeerContract from 0x03

transaction() {

  prepare(signer: AuthAccount) {
    //create beer
    let testBeer <- BeerContract.createBeer()

    //save beer
    signer.save(<- testBeer, to: /storage/MyBeers)

    //load beer
    let newRefBeer = signer.borrow<&BeerContract.Beer>(from: /storage/MyBeers) ?? panic("Could not load Beer Item")

    //log name of beer
    log(newRefBeer.name)
  }

  execute {  }
}
```


-----------------------------------------------------------------------------------------------------------------------------



### Chapter 4
### Day 2

What does .link() do?
  - .link creates an either private or public link to share information about your account storage to other people. It sepcifies what type of object you are looking for, where to look for it, and what capabilities it should have when accessing it

In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.
 - A resource interface will allow us to have a list of certain actions we want the public to be able to perform, or attributes they can read, without allowing them access to information that they don't need or shouldn't have. This would be useful in "Roles" situations/ For example,  where Managers could need access to certain staff information that Sales Representatives or Serving Staff should not have.

Deploy a contract that contains a resource that implements a resource interface. Then, do the following:
```cadence
pub contract BeerContract {

    pub resource interface IBeerPublic {
        pub var name : String
    }
    
    pub resource Beer : IBeerPublic {
        pub var name : String

        pub fun changeName(_newName: String){
            self.name = _newName
        }
        
        init() {
            self.name = "Spike's Corners IPA"
        }
    }

    pub fun createBeer(): @Beer {
        return <- create Beer()
    }

    init() {
    }
}

```
In a transaction, save the resource to storage and link it to the public with the restrictive interface.
```cadence
import BeerContract from 0x03

transaction() {
  prepare(signer: AuthAccount) {
  
    let baseBeerStorage = /storage/MyBeers
    let publicPath = /public/MyBeersPublic
    let privatePath = /private/MyBeersPrivate

    //save beer
    signer.save(<- BeerContract.createBeer(), to: baseBeerStorage)

    signer.link<&BeerContract.Beer{BeerContract.IBeerPublic}>(publicPath, target: baseBeerStorage)
  }

  execute {  }
}

```
Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.

![image](https://user-images.githubusercontent.com/5509347/173915941-2c9996d8-b8ed-4278-b3eb-3791f4431b55.png)

Run the script and access something you CAN read from. Return it from the script.
![image](https://user-images.githubusercontent.com/5509347/173916168-78b1f4e3-56ef-4698-befe-2854255b64a7.png)



-----------------------------------------------------------------------------------------------------------------------------



### Chapter 4
### Day 3

Why did we add a Collection to this contract? List the two main reasons.
  - This allows the public access to our storage so they can view and deposit information into our collection in a manner we specify.
  - This will separate our stored items in one central location rather than having to specify a new storage path each time. This allows us to separate our data from other data as well.

What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")
 - If a reource is destroyed, any resources contained inside that resource must also be destroyed unless they are explicitly moved first.

Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.
 - If anyone can mint an NFT, then there is no value to them. Only one account should be in charge of minting and distributing NFT's originally. If we made a "Minter" resource and gave the CreateNFT functionality only to that minter, only an account with that "Minter" resource could create new NFT's.

 - If we have to read information from an NFT, we are currently only able to withdraw, read, then deposit back. This uses unnecessary power, and adds the possibility of the item getting misused. If we had a function to return a reference to an NFT at a certain ID we could access whatever information we wanted, without moving the item from the collection.




-----------------------------------------------------------------------------------------------------------------------------



### Chapter 4
### Day 4

```cadence
pub contract CryptoPoops {
  pub var totalSupply: UInt64 //the current total supply of NFT's made available. Will start at 0 and increase when minted

  // This is an NFT resource that contains a name,
  // favouriteFood, and luckyNumber
  pub resource NFT {
    pub let id: UInt64 //NFT id number

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    //initialize all variables
    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid

      self.name = _name
      self.favouriteFood = _favouriteFood
      self.luckyNumber = _luckyNumber
    }
  }

  // This is a resource interface that allows us to restrict public access to our NFT's when iplementing it
  // The public is allowed to: See NFT ID's, Borrow Data abouy an NFT at a certain ID, and Deposit an NFT
  pub resource interface CollectionPublic {
    pub fun deposit(token: @NFT)
    pub fun getIDs(): [UInt64]
    pub fun borrowNFT(id: UInt64): &NFT
  }

  // This is a resource for our Collection of NFT's. It will contain all our NFT items.
  pub resource Collection: CollectionPublic {
    pub var ownedNFTs: @{UInt64: NFT}  //Dictionary of NFT items available in this collection

    //Function to deposit an NFT into our collection, accessible to the public
    pub fun deposit(token: @NFT) {
      self.ownedNFTs[token.id] <-! token
    }

    //Function to withdraw an NFT from our collection at a certain ID number
    pub fun withdraw(withdrawID: UInt64): @NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
              ?? panic("This NFT does not exist in this Collection.")
      return <- nft
    }

    //function to ge a list of ID's from the collection
    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    //function to return a reference to an NFT item for data viewing, without moving it from storage
    pub fun borrowNFT(id: UInt64): &NFT {
      return &self.ownedNFTs[id] as &NFT
    }

    //initialize our empty collection
    init() {
      self.ownedNFTs <- {}
    }

    //destroy our collection of NFT's when our Collection is destroyed
    destroy() {
      destroy self.ownedNFTs
    }
  }

  //create an empty collection and return it
  pub fun createEmptyCollection(): @Collection {
    return <- create Collection()
  }

  //This is the Minter Resource, which will be the only reource allowed to Create an NFT via a function call
  // It is also allowed to create another minter if it wishes to pass the permissio along
  pub resource Minter {

    //Creates an NFT and returns it
    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    //creates a Miner and retuns it
    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

  //initialize the contract, create a Minter resorce and save it to the account which deployed the contract in order to provide that user minting capability
  init() {
    self.totalSupply = 0
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}
```





-----------------------------------------------------------------------------------------------------------------------------



### Chapter 5
### Day 1


Describe what an event is, and why it might be useful to a client.
  - Events allow a contract to communicate that somthing has happened to a client without them having to continuously ask if it happened. It's like having kids always ask "Are we there yet?".... we will let you know when we are there, just listen for when we tell you we are there.

Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened.
```cadence
pub contract BeerContract {
    pub event createdBeer()

    pub resource interface IBeerPublic {
        pub var name : String
    }
    
    pub resource Beer : IBeerPublic {
        pub var name : String
        
        pub fun changeName(_newName: String){
            self.name = _newName
        }
        
        init() {
            self.name = "Spike's Corners IPA"
        }
    }

    pub fun createBeer(): @Beer {
        emit createdBeer()
        return <- create Beer()
    }

    init() {
    }
}
```

Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.
```cadence
pub fun changeName(_newName: String){
  pre{
      _newName.length > 0 : "Name not long enough"
  }
  self.name = _newName
}

pub fun getName() : String {
  post{
      result != "" : "Name is empty"
  }
  let gotName = self.name
  return gotName
}
```

For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.
```cadence
pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name) //YES this will log the name, because "Jacob" is 5 letters long
  }

  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name." //Pass, the name length is greater than 0
    }
    post {
      result == "Jacob Tucker" //Pass, the function will concatenate the name into "Jacob Tucker", then we check the value at the end and it is equal
    }
    return name.concat(" Tucker") //This function will return this value
  }

  pub resource TestResource {
    pub var number: Int

    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
    
    // - This function will not log the number, it will error
    // if number == 0 then once we call the funtion, it will increment to 1, try and return 1, find that 0 != 2 and then error
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }
  }
}
```






-----------------------------------------------------------------------------------------------------------------------------



### Chapter 5
### Day 2

Explain why standards can be beneficial to the Flow ecosystem.
 - Standards are beneficial anywhere. It gives everyone a set of guidlines to follow in order to understand things better. A standard defines what something is. If I make a beer, it has to be a beer. I cannot make a cider and call it a beer because there are standards for each. They may both meet the requirements for a more general "Fermented Beverage" standard however. This ensures the consumer knows what they are drinking, and what the ingredients are. If bleach met the beer standard, we would all be in trouble.
 - If there is a standard for the way NFT's are built, then they should all function simlarly and be able to communicate with eath other on a basic level fairly easily, making growth of the system much easier.


What is YOUR favourite food?
self.favouriteFood = Hamburgers

Please fix this code (Hint: There are two things wrong):

The contract interface:
```cadence
pub contract interface ITest {
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    pre {
      newNumber >= 0: "We don't like negative numbers for some reason. We're mean."
    }
    post {
      self.number == newNumber: "Didn't update the number to be the new number."
    }
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff : IStuff {    //WAS not implementing the IStuff interface
    pub var favouriteActivity: String
  }
}
```

The implementing contract:
```cadence
Import ITest from _address_ //have to import contract interface to implement it
pub contract Test : ITest {       //WAS not actually implementing the contrt interface
  pub var number: Int
  
  pub fun updateNumber(newNumber: Int) {
    self.number = 5
  }

  pub resource interface IStuff {
    pub var favouriteActivity: String
  }

  pub resource Stuff: ITest.IStuff {   // MUST be implementing the ITest.IStuff interface, not our own now that we are using the ITest contract interface
    pub var favouriteActivity: String

    init() {
      self.favouriteActivity = "Playing League of Legends."
    }
  }

  init() {
    self.number = 0
  }
}
```






-----------------------------------------------------------------------------------------------------------------------------



### Chapter 5
### Day 3


What does "force casting" with as! do? Why is it useful in our Collection?
- Force Casting tells the code what type we are using in our collection, and if the generic NFT doesn't meet that standard then to panic. This is important to ensure that whatever we are depositing into our collection is something that is part of our collection. I should not be able to deposit a "Goated Goat" into my Beer NFT collection, because that would just be weird, and I may not find it again or know what to do with it inside that collection.

What does auth do? When do we use it?
 - In order to downcast a reference using the as! operator, we must have that reference be authorized. using the as auth declaration gets an authorized reference to that object which we can then downcast.

UPDATED CONTRACT, TRANSACION AND SCRIPT:

```cadence
import NonFungibleToken from 0x02
pub contract CryptoPoops: NonFungibleToken {
  pub var totalSupply: UInt64

  pub event ContractInitialized()
  pub event Withdraw(id: UInt64, from: Address?)
  pub event Deposit(id: UInt64, to: Address?)

  pub resource NFT: NonFungibleToken.INFT {
    pub let id: UInt64

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid

      self.name = _name
      self.favouriteFood = _favouriteFood
      self.luckyNumber = _luckyNumber
    }
  }

  //added implementation of ICollectionPublic
  pub resource Collection: NonFungibleToken.Provider, NonFungibleToken.Receiver, NonFungibleToken.CollectionPublic, ICollectionPublic  {
    pub var ownedNFTs: @{UInt64: NonFungibleToken.NFT}

    pub fun withdraw(withdrawID: UInt64): @NonFungibleToken.NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
            ?? panic("This NFT does not exist in this Collection.")
      emit Withdraw(id: nft.id, from: self.owner?.address)
      return <- nft
    }

    pub fun deposit(token: @NonFungibleToken.NFT) {
      let nft <- token as! @NFT
      emit Deposit(id: nft.id, to: self.owner?.address)
      self.ownedNFTs[nft.id] <-! nft
    }

    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    pub fun borrowNFT(id: UInt64): &NonFungibleToken.NFT {
      return (&self.ownedNFTs[id] as &NonFungibleToken.NFT?)!
    }

    //added this function
    pub fun borrowAuthNFT(id: UInt64): &NFT {
      let ref = (&self.ownedNFTs[id] as auth &NonFungibleToken.NFT?)!
      return ref as! &NFT
    }

    init() {
      self.ownedNFTs <- {}
    }

    destroy() {
      destroy self.ownedNFTs
    }
  }

  pub fun createEmptyCollection(): @NonFungibleToken.Collection {
    return <- create Collection()
  }

  pub resource Minter {

    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

  //Added this reource interface to allow for public detailed NFT reading
  pub resource interface ICollectionPublic {
        pub fun getIDs() : [UInt64]
        pub fun deposit(token: @NonFungibleToken.NFT)
        pub fun borrowNFT(id: UInt64): &NonFungibleToken.NFT
        pub fun borrowAuthNFT(id: UInt64): &NFT
    }

  init() {
    self.totalSupply = 0
    emit ContractInitialized()
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}
```


MINT & STORE NFT TRANSACTION
```cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

transaction (recipient: Address, name: String, favouriteFood: String, luckyNumber: Int) {
  
    prepare(acct: AuthAccount) {
        let nftMinter = acct.borrow<&CryptoPoops.Minter>(from: /storage/Minter) ?? panic("Could not get NFT Minter")

        //Get Collection to add NFT to Collection
        let publicRef = getAccount(recipient).getCapability(/public/MyCollection)
                                        .borrow<&CryptoPoops.Collection{CryptoPoops.ICollectionPublic}>()
                                        ?? panic("This account does not have a collection.")

        //Mint an NFT
        let nft <- nftMinter.createNFT(name: name, favouriteFood: favouriteFood, luckyNumber: luckyNumber)

        //Deposit an NFT
        publicRef.deposit(token: <- nft)
    }

    execute {
        log("Stored a new NFT into Collection")
    }
}
```

GET ID's Script
```cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

pub fun main(account: Address) {
  let publicRef = getAccount(account).getCapability(/public/MyCollection)
                                      .borrow<&CryptoPoops.Collection{CryptoPoops.ICollectionPublic}>()
                                      ?? panic("Could not borrow NFT Collection")

  log(publicRef.getIDs())
  
}
```

READ METADATA TRANSACTION
```cadence
import CryptoPoops from 0x01
import NonFungibleToken from 0x02

pub fun main(account: Address, id: UInt64) {
  let publicRef = getAccount(account).getCapability(/public/MyCollection)
                                      .borrow<&CryptoPoops.Collection{CryptoPoops.ICollectionPublic}>()
                                      ?? panic("Could not borrow NFT Collection")

  let ref = publicRef.borrowAuthNFT(id: id)
  log(ref.id)
  log(ref.name)
  log(ref.favouriteFood)
  log(ref.luckyNumber)  
}
```









