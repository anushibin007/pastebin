# PS07Q1 Design Document

## Author // Student ID

Anu Shibin J // 2022MT12007

## Design Analysis

-   This `CustomHashTable` has the following items:  
     a. An `ArrayList` to hold the items as chains. The items are stored in chains using the **Separate Chaining** method in these buckets to avoid collision.  
     b. All the other remaining functions like `hashId(String)`, `add(Application)`, `remove(String applicationName)`, etc to perform operations on the HashTable.
-   The `hashId(String)` function generates the hash of a `String` by adding the ASCII value of each character in the `String` to the hash generated in each previous character iteration. We also multiply 31 to this hash in order to avoid collisions as much as possible. The number 31 was chosen because it as an odd-prime number and is mathematically proven to cause lesser collisions and is recommended by Oracle too. The Hashing function used can be defined as:

```
h(k) = 31 * h(x) + ASCII(k)
```

## Time Complexity Analysis

**Note:** Please check the inline comments in the code to indentify how each individual operation consumes said amount of time.

| Function           | Time Complexity                                  | Comment                                                                                                                                                                     |
| ------------------ | ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `hashId`           | O(N)                                             | Where N is the number of characters in the String that needs to be hashed                                                                                                   |
| `initializeHash`   | O(1)                                             | Since there will be only one bucket initially                                                                                                                               |
| `insertAppDetails` | O(N) + O(N) + O(1) + O(M) + O(1) + O(N) = O(N+M) | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed                                                    |
| `updateAppDetails` | O(N+M) + O(5) + O(N+M) = O(N+M)                  | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed                                                    |
| `memRef`           | O(M+N)                                           | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed                                                    |
| `appStatus`        | O(M+N+Q)                                         | Where N is the number of buckets and M is the number of items in the chain in a bucket where the given hashId is indexed and Q is the number of different application types |
| `destroyHash`      | O(N)                                             | Where N is the number of buckets                                                                                                                                            |

## Instructions to run the program
<ol>
<li>Paste the input and prompt files <code>inputPS07Q1.txt</code> & <code>promptsPS07Q1.txt</code> respectively into the folder where the the java source file (<code>PS07Q1.java</code>) is present</li>
<li>Compile the java file using the command</li>
```
java PS07Q1.java
```
<li>Run the program using the command</li>
```
javac PS07Q1
```
<li>The output will be printed to the file <code>outputPS07Q1.txt</code></li>
</ol>
**Note:** The sample input and output files are already provided in the ZIP.
