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








