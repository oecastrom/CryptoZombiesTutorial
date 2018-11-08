# CryptoZombiesTutorial
CryptoZombies tutorial 

## Definitions 
1. **contract**: Fundamental building block of Ethereum applications - all variables and functions belong to a **contract**.

        ```
        contract Contract {

         }
        ```

2. Version Pragma: A declaration of the version of the Solidity compiler this code should use. Used to prevent issues with future compiler version potentially introducing changes that would break your code.

        ```
        pragma solidity ^0.4.19;
        ```

3. State variables: Are permanently stored in contract storage. This means they're written to the Ethereum blockchain - think of them like writing to a DB.

4. Unsigned Integers: The **uint** data type is an usigned integer, meaning its value must be non-negative. There is also an **int** data type for signed integers. Note that **uint** is an alias for **uint256**, a 256-bit integer. You can declare uint with less bits - **uint8**, **uint16**, **uint32**, etc. 

5. Math Operators: 

        ```
        Addition: +
        Subtraction: -
        Multiplication: *
        Division: /
        Modulo: %
        Exponentiation: **
        ```

6. **struct**: A more complex data type - allows you to create more complicated data types that have multiple properties.

        ``` 
        struct Person {
            uint age;
            string name;
        }
        ```

7. **string**: Used for arbitrary-length UTF-8 data

8. Arrays: A collection of something. There are two types of arrays in Solidity - **fixed** and **dynamic**. Note you can also create an array of structs and declare an array as **public** (other contracts are able to read but not write to this array) which Solidity in turn then creates a getter method for it automatically.

        ```
        // Array with a fixed length of 2 elements
        uint[2] fixedArray;

        // Another fixed Array, can contain 5 strings
        string[5] stringArray;

        // A dynamic Array - has no fixed size, can keep growing
        uint[] dynamicArray;

        // Dynamic Array, we can keep adding to it
        Person[] public people; 
        ```

9. Function Declarations: Note - It's convention (but not required) to start function parameter variable names with an underscore ( **_** ) in order to differentiate them from global variables. 

        ```
        function eatHamburgers(string _name, uint _amount) {

        }
        ```

10. **private** & **public** Functions: Functions are **public** by default, this means anyone or any other contract can call your contract's function and execute its code (this is not always desirable, as it can make your contract vulnerable to attacks). This is why it is good practice to make your functions **private** by default. Private functionality allows only other functions within our contract to call other functions. Note - It's convetion to start private function names with an underscore ( **_** ).


11. Function **return** Values: To **return** a value from a function, the declartion looks like the following - 

        ```
        string greeting = "Hello";

        function sayHello() public view returns (string) {
            return greeting;
        }
        ```

The function declaration contains the type of the return value. 

12. **view** & **pure** Function Modifies: The example in 11. doesnt actually change state in Solidity e.g. It doesnt change any values or write anything. So in this case we could declare it as a **view** function, meaning it's only viewing the data but not modifying it. Solidity also contains **pure** functions, which means you're not even accessing any data in the app. Consider the following 

        ```
        function _multiply(uint a, uint b) private pure returns (uint){
            return a * b;
        }
        ```

This function doesn't read the state of the app - its return value depends only on its function parameters. So in this case we would declare the function as **pure**.

13. Keccak256: Hash function built into Ethereum which is a version of SHA3. A has function basically maps an input **string** into a random 256-bit hexidecimal number. A slight change in the **string** will cause a large change in the hash. 

14. Typecasting: When you need to convert between data types.

        ```
        uint8 a = 5;
        uint b = 6;

        uint8 c = a * uint8(b);
        ```

15. **event**: Events are a way for your contract to communicate that something happened on the blockchain to your app front-end, which can be 'listening' for certain events and take action when they happen.

        ```
        // Declare the event
        event IntegersAdded(uint x, uint y, uint result);

        function add(uint _x, uint _y) public {
                uint result = _x + _y;

                // Fire an event to let the app know the function was called
                IntegersAdded(_x, _y, result);
                return result;
        }
        ```

Your app front-end could then listen to the event. A javascript implementation would look something like:

        ```
        myContract.IntegersAdded(function(error, result) {
                // Do something with result
        })
        ```

16. **Web3.js**: Javascript library with a collection of modules that contain specific functionality for the Ethereum ecosystem. 

17. **address**: A unique identifier that points to an Ethereum account (a user or a smart contract) usually having a balance of Ether. You can send and receiver Ether payments to and from other addresses. 

        ```
        0xC1Aa4B2c9e4D0fDE29E65b8a0F70603c6B46c70b
        ```

18. **mapping**: Mappings are another way of storing organized data in Solidity. It is essentially a key-value store for storing and looking up data. In the following example, they key is an **address** and the value is a **uint**, in the second example the key is a **uint* and the value a **string**.

        ```
        // For a financial app, storing a uint that holds the user's account balance
        mapping (address => uint) public accountBalance;

        // Or could be used to store / lookup usernames based on userId
        mapping (uint => string) userIdToName;
        ```
19. **msg.sender**: In Solidity, there certain global variables that are available to all functions. One of these is **msg.sender**, which refers to the **address** of the person (or smart contract) who called the current function. Note - in Solidity, function execution always needs to start with an external caller. A contract will just sit on the blockchain doing nothing until someone calls one of its functions. So there will always be a **msg.sender**.

20. **require**: Require makes it so that the function will throw an error and stop executing if some condition is **not true**.

        ```
        function sayHiToVitalik(string _name) public returns (string) {

        // Compares if _name equals "Vitalik". Throws an error and exits if not true. (Side note: Solidity doesn't have native string comparison, so we compare their keccak256 hashes to see if the strings are equal)

                require(keccak256(_name) == keccak256("Vitalik"));

        // If it's true, proceed with the function
                return "Hi!";
        }
        ```

If you call this function with sayHiToVitalik("Vitalik"), it will return "Hi!". If you call it with any other input, it will throw an error and not execute.

21. Inheritance: Rather than making one extremely long contract, sometimes it makes sense to split your code logic across multiple contracts to organize the code. One feature of Solidity that makes this more manageable is contract **inheritance**

        ```
        contract Doge {
                function catchphrase() public returns (string) {
                        return "So Wow CryptoDoge";
                 }
        }

        contract BabyDoge is Doge {
                function anotherCatchphrase() public returns (string) {
                        return "Such Moon BabyDoge";
                }
        }

BabyDoge inherits from Doge. That means if you compile and deploy BabyDoge, it will have access to both catchphrase() and anotherCatchphrase() (and any other public functions we may define on Doge). This can be used for logical inheritance (such as with a subclass, a Cat is an Animal). But it can also be used simply for organizing your code by grouping similar logic together into different contracts.

22. **import**: When you have multiple files and you want to import one file into another, Solidity uses the **import** keyword.

        ```
        import "./SomeOtherContract.sol";

        contract newContract is SomeOtherContract {

        }
        ```

So if we had a file named someothercontract.sol in the same directory as this contract (that's what the ./ means), it would get imported by the compiler.

23. **storage** vs **memory**: In Solidity, there are two places you can store variables - in **storage** and in **memory**. **storage** refers to variables stored permanently on the blockchain. **memory** variables are temporary, and are erased between external function calls to your contract. Think of it like your computer's hard disk vs RAM. Most of the time you don't need to use these keywords because Solidity handles them by default. State variables (variables declared outside of functions) are by default storage and written permanently to the blockchain, while variables declared inside functions are memory and will disappear when the function call ends. However, there are times when you do need to use these keywords, namely when dealing with structs and arrays within functions:

        ```
        contract SandwichFactory {
                struct Sandwich {
                        string name;
                        string status;
                }

                Sandwich[] sandwiches;

                function eatSandwich(uint _index) public {
                        // Sandwich mySandwich = sandwiches[_index];
                        // ^ Seems pretty straightforward, but solidity will give you a warning telling you that you should explicitly declare `storage` or `memory` here.

                        // So instead, you should declare with the `storage` keyword, like:

                        Sandwich storage mySandwich = sandwiches[_index];

                        // ...in which case `mySandwich` is a pointer to `sandwiches[_index]` in storage, and...

                        mySandwich.status = "Eaten!";

                        // ...this will permanently change `sandwiches[_index]` on the blockchain.

                        // If you just want a copy, you can use `memory`:

                        Sandwich memory anotherSandwich = sandwiches[_index + 1];

                        // ...in which case `anotherSandwich` will simply be a copy of the data in memory, and...

                        anotherSandwich.status = "Eaten!";

                        // ...will just modify the temporary variable and have no effect on `sandwiches[_index + 1]`. But you can do this:

                        sandwiches[_index + 1] = anotherSandwich;

                        // ...if you want to copy the changes back into blockchain storage.
                }
        }

24. **internal** vs **external**: In addition to **public** and **private**, Solidity has two more types of visibility for functions - **internal** and **external**. **internal** is the same as **private**, except that it's also accessible to contracts that inherit from this contract. **external** is similar to **public**, except that these functions can ONLY be called outside the contract - they can't be called by other functions inside that contract. 

        ```
        contract Sandwich {
                uint private sandwichesEaten = 0;

                function eat() internal {
                        sandwichesEaten++;
                }
        }

        contract BLT is Sandwich {
                uint private baconSandwichesEaten = 0;

                function eatWithBacon() public returns (string) {
                        baconSandwichesEaten++;
                        // We can call this here because it's internal
                        eat();
                }
        }
        ```

25. **interface**: