# PS07Q1 Design Document

## Author
Anu Shibin J

## Student ID
2022MT12007

## Design Analysis
1. The first thing that the program does is clear the output file `outputPS07Q1.txt`.
2. Then it reads the input data from the `inputPS07Q1.txt` file.
3. The custom implementation of the HashTable is an inner class called `CustomHashTable`.
4. This `CustomHashTable` has the following items:  
		a. An `ArrayList` to hold the items as chains. The items are stored in chains in these buckets to avoid collision.  
		b. All the other remaining functions like `hashId(String)`, `add(Application)`, `remove(String applicationName)`, etc to perform operations on the HashTable.  
5. The `hashId(String)` function generates a hash of a `String` by adding the ASCII value of each character in the `String` to the hash generated in each previous character iteration. We also multiply 31 to this hash in order to avoid collisions as much as possible. The number 31 was chosen because it as an odd-prime number and is mathematically proven to cause lesser collisions and is recommended by Oracle too.
6. 

## Complexity Analysis
### Time Complexity
Please check the inline comments in the code to indentify how each individual operation consumes said amount of time.

| Function           | Time Complexity                                  | Comment                                                                                                                                                                     |
| ------------------ | ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `hashId`           | O(N)                                             | Where N is the number of characters in the String that needs to be hashed                                                                                                   |
| `initializeHash`   | O(1)                                             | Since there will be only one bucket initially                                                                                                                               |
| `insertAppDetails` | O(N) + O(N) + O(1) + O(M) + O(1) + O(N) = O(N+M) | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed                                                    |
| `updateAppDetails` | O(N+M) + O(5) + O(N+M) = O(N+M)                  | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed                                                    |
| `memRef`           | O(M+N)                                           | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed                                                    |
| `appStatus`        | O(M+N+Q)                                         | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed and Q is the number of different application types |
| `destroyHash`      | O(N)                                             | Where N is the number of buckets                                                                                                                                            |

### Space Complexity

## Instructions to run the program