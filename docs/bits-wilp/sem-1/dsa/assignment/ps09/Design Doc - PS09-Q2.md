# PS07Q2 Design Document

## Author
Varshinni M

## Student ID
2022MT12505

## Design Analysis
-   This problem can be solved using a type of greedy algorithm called as the **Unbound Knapsack Problem** algorithm.
- The "greedy" aspect of this approach is that we are sorting the given ammunitions based on their respective damage/weight ratio. We are "greedy" for the ammo that can cause the most damage per unit weight.
- The code has 2 main components:
	- The `main(...)` method, which is the driver method.
	- The `getMaxDamage(...)` method, which has the core business logic of the program, which executes the greedy algorithm to compute the max damage possible for the given ammo for the given max capacity.

## Time Complexity Analysis
We need to consider the following operations in the `getMaxDamage(...)` method:  

1. A sort that takes `O(N log N)` in the worst case. Where `N` is the number of ammunition types.  
2. An iteration through each item in the "knapsack" to compute how many of them can be carried. In the worst case, we go through every item. So, the time complexity becomes `O(N)`. Where `N` is the number of ammunition types.  

Hence, the final time complexity becomes:
```
O(N log N) + O(N) = O(N log N)
```
where `N` is the number of ammunition types.
## Instructions to run the program
<ol>
<li>Paste the input file <code>inputPS07Q2.txt</code> into the folder where the the java source file (<code>PS07Q2.java</code>) is present</li>
<li>Compile the java file using the command</li>
```
java PS07Q2.java
```
<li>Run the program using the command</li>
```
javac PS07Q2
```
<li>The output will be printed to the file <code>outputPS07Q2.txt</code></li>
</ol>
**Note:** The sample input and output files are already provided in the ZIP.
