# CryptoZombiesTutorial
CryptoZombies tutorial 

# Definitions 
1. contract: Fundamental building block of Ethereum applications - all variables and functions belong to a contract.

    Ex. 
        contract Contract {

         }

2. Version Pragma: A declaration of the version of the Solidity compiler this code should use. Used to prevent issues with future compiler version potentially introducing changes that would break your code.

    Ex. 
        pragma solidity ^0.4.19;

3. State variables: Are permanently stored in contract storage. This means they're written to the Ethereum blockchain - think of them like writing to a DB.

4. Unsigned Integers: The uint data type is an usigned integer, meaning its value must be non-negative. There is also an int data type for signed integers. Note that uint is an alias for uint256, a 256-bit integer. You can declare uint with less bits - uint8, uint16, uint32, etc. 

5. Math Operators: +, -, *, /, %, **

6. structs: A more complex data type - allows you to create more complicated data types that have multiple properties.

    Ex. 
        struct Person {
            uint age;
            string name;
        }

7. string: Used for arbitrary-length UTF-8 data

8. Arrays: A collection of something. There are two types of arrays in Solidity - fixed and dynamic. Note you can also create an array of structs and declare an array as public (other contracts are able to read but not write to this array) which Solidity in turn then creates a getter method for it automatically.

    Ex. 
        // Array with a fixed length of 2 elements
        uint[2] fixedArray;

        // Another fixed Array, can contain 5 strings
        string[5] stringArray;

        // A dynamic Array - has no fixed size, can keep growing
        uint[] dynamicArray;

        // Dynamic Array, we can keep adding to it
        Person[] public people; 

9. Function Declarations: Note - It's convention (but not required) to start function parameter variable names with an underscore ( _ ) in order to differentiate them from global variables. 

    Ex. function eatHamburgers(string _name, uint _amount) {

        }

10. private & public Functions: Functions are public by default, this means anyone or any other contract can call your contract's function and execute its code (this is not always desirable, as it can make your contract vulnerable to attacks). This is why it is good practice to make your functions private by default. Private functionality allows only other functions within our contract to call other functions. Note - It's convetion to start private function names with an underscore ( _ ).


11. Function return Values: To return a value from a function, the declartion looks like the following - 

    Ex.
        string greeting = "Hello";

        function sayHello() public view returns (string) {
            return greeting;
        }

The function declaration contains the type of the return value. 

12. view & pure Function Modifies: The example in 11. doesnt actually change state in Solidity e.g. It doesnt change any values or write anything. So in this case we could declare it as a view function, meaning it's onyl viewing the data but no midifying it. Solidity as contains pure functions, which means you're not even accessing any data in the app. Consider the following 

    Ex. 
        function _multiply(uint a, uint b) private pure returns (uint){
            return a * b;
        }

This function doesn't read the state of the app - its return value depends only on its function parameters. So in this case we would declare the function as pure.

13. Keccak256: Hash function built into Ethereum which is a version of SHA3. A has function basically maps an input string into a random 256-bit hexidecimal number. A slight change in the string will cause a large change in the hash. 

14. Typecasting: 