# PS09Q2 Design Document

## Author
Varshinni M

## Student ID
2022MT12505

## Design Analysis
This problem can be solved using a direct greedy approach where we consider one good dish to be ready if we find matching number of ingredients. This is opposed to a brute force approach because we are not calculating permutations or combinations of possible good disher. Rather, we are *greedily* looking for a matching number of ingredients in the given input.

## Time Complexity Analysis
We need to iterate through all the ingredients in a given input. Hence, the time complexity of this algorithm is:
```
O(N)
```
where N is the number of ingredients in a given input. For example, for the input `SPPPPSSSPS`, N is 10.

## Instructions to run the program
<ol>
<li>Paste the input file <code>inputPS09Q2.txt</code> into the folder where the the java source file (<code>PS09Q2.java</code>) is present</li>
<li>Compile the java file using the command</li>
```
java PS09Q2.java
```
<li>Run the program using the command</li>
```
javac PS09Q2
```
<li>The output will be printed to the file <code>outputPS09Q2.txt</code></li>
</ol>
**Note:** The sample input and output files are already provided in the ZIP.
