# CryptoZombiesTutorial
CryptoZombies tutorial 

# Definitions 
1. contract: Fundamental building block of Ethereum applications - all variables and functions belong to a contract.

    Ex. contract Contract {

    }

2. Version Pragma: A declaration of the version of the Solidity compiler this code should use. Used to prevent issues with future compiler version potentially introducing changes that would break your code.

    Ex. pragma solidity ^0.4.19;

3. State variables: Are permanently stored in contract storage. This means they're written to the Ethereum blockchain - think of them like writing to a DB.

4. Unsigned Integers: The uint data type is an usigned integer, meaning its value must be non-negative. There is also an int data type for signed integers. Note that uint is an alias for uint256, a 256-bit integer. You can declare uint with less bits - uint8, uint16, uint32, etc. 

5. Math Operators: +, -, *, /, %, **

6. structs: A more complex data type - allows you to create more complicated data types that have multiple properties.

    Ex. struct Person {
        uint age;
        string name;
    }

7. string: Used for arbitrary-length UTF-8 data

8. Arrays: A collection of something. There are two types of arrays in Solidity - fixed and dynamic. Note you can also create an array of structs and declare an array as public (other contracts are able to read but not write to this array) which Solidity in turn then creates a getter method for it automatically.

    Ex. // Array with a fixed length of 2 elements
        uint[2] fixedArray;

        // Another fixed Array, can contain 5 strings
        string[5] stringArray;

        // A dynamic Array - has no fixed size, can keep growing
        uint[] dynamicArray;

        // Dynamic Array, we can keep adding to it
        Person[] public people; 

9. Function Declarations: