# PS09Q1 Design Document

## Author
Varshinni M

## Student ID
2022MT12505

## Design Analysis

- We use an `ArrayList` as a "database" to store all the citizens that need to be processed. Once a Citizen has been processed, they are removed from this list.
- The Max heap is implemented using the technique of **Priority Queue** and is represented as an array of `CitizenRecord` objects.
- We can store upto a max of 100 items in the MaxHeap. This value can be altered by changing the value of the constant `ARRAY_MAX_CAPACITY`. If we try to push more than 100 items (by default), an `ArrayIndexOutOfBoundsException` will be thrown saying "`Heap limit reached`".

## Design Considerations
- An ambiguity in the question was whether to throw an error when we try to invoke `nextCitizen()` when the records in the Queue get depleted. This was solved by printing the statement "`End of Queue`" when such a scenario occurs.
- The main and only deviation in this problem statement is that not only does the root of the heap need to have the max item in the heap but also every item in the heap must also be always sorted according to the given priority. Hence, we have to do a **Heap Sort** after every insert or delete operation.
- We should ideally perform a Heap Sort in order to sort every element in the queue according to its priority whenever a new record is added. That is kind of an "active" sorting approach to keep the queue sorted at all time. But that increases the time complexity of the algorithm by a huge factor. Also, there is no point in sorting the heap during insertion because we are not *reading* any data from they queue yet. Hence, we will do a "lazy-sort" - meaning that we will sort the items only when needed - that is, either when performing *read* operations like looking for the next Citizen or when printing the queue.

## Time Complexity Analysis

| Function          | Time Complexity | Comment                                                                        |
| ----------------- | --------------- | ------------------------------------------------------------------------------ |
| `registerCitizen` | O(N log N)      | Where N is the number of initial Citizens                                      |
| `enqueueCitizen`  | O(1)            | Since we are just inserting an item into the i<sup>th</sup> index in the Queue |
| `nextCitizen`     | O(N log N)      | Where N is the number Citizens currently in the Queue                                    |
| `dequeueCitizen`  | O(N)            | Where N is the number Citizens currently in the Queue                                     |

## Instructions to run the program
<ol>
<li>Paste the input files <code>inputPS09Q1a.txt</code> & <code>inputPS09Q1b.txt</code> respectively into the folder where the the java source file (<code>PS09Q1.java</code>) is present</li>
<li>Compile the java file using the command</li>
```
java PS09Q1.java
```
<li>Run the program using the command</li>
```
javac PS09Q1
```
<li>The output will be printed to the file <code>outputPS09Q1.txt</code></li>
</ol>
**Note:** The sample input and output files are already provided in the ZIP.
