# PS20-Q1-Chegg-Solution

## Problem Statement
Please check the PDF. It is too long.

## [Chegg](https://www.chegg.com/homework-help/questions-and-answers/1-problem-statement-government-hospital-treating-patients-covid-management-preparing-token-q52072278) Solution:

Let's say Package_folder_name = 1

A1_PS6_DC_1.py

***********************************************************************************************************************************

```python
#!/usr/bin/env python3

import copy
import re


class PatientRecord:
""" Stores patient info. """

def __init__(self, age, name, Pid):
self.PatId = str(Pid) + str(age).rjust(2, '0')
self.name = name
self.age = age
self.left = None
self.right = None

def __str__(self):
""" debugging aid """
return "{}, {}, {}".format(self.name, self.age, self.PatId)


def next_patient_banner(p):
""" Generate 'Next Patient' message.
Return info about the next patient.
"""

if p is None:
return "Patient queue is empty.\n"

return """---- next patient ---------------
Next patient for consultation is: {}, {}
----------------------------------------------
""".format(p.PatId, p.name)


def _swap(n1, n2):
""" Swap two nodes. """

# It is easier to swap the values than all the links.
n1.age, n2.age = n2.age, n1.age
n1.name, n2.name = n2.name, n1.name
n1.PatId, n2.PatId = n2.PatId, n1.PatId


def _max(node1, node2):
""" Return the node having higher age value,
or None if both nodes do not exist.
"""

if node1 is None and node2 is None:
return None

if node1 is None:
return node2
if node2 is None:
return node1

if node1.age > node2.age:
return node1
else:
return node2


def read_in2():
""" Read the second input file, line by line. """

infile = 'inputPS5b.txt'
with open(infile, "r") as f:
for line in f:
yield line
return


def write_out2(file):
""" Write/append to second output file. """

outfile = 'outputPS5.txt'
with open(outfile, "a+") as f:
f.write(file)
return


class ConsultQueue:
""" Build the Consult Queue as a max heap tree.
For every new patient, the patient id is generated and
it's record inserted to heap tree and the tree is heapified.
"""

initial_pid = pid = 1000 # patient counter (initial value.)
register = dict() # provide easy mapping b/w patId and patient node.
queue = list() # stores the max heap tree
queue2 = list() # duplicate list, preserves the original heap for reconstruction.
root = None # heap tree's root

def registerPatient(self, name, age):
""" Register a patient node.
- generate a patient ID
- add the patient node to a max heap tree.
Return newly added patient node.
"""

patid = self._generate_pat_id()
patient = PatientRecord(age, name, patid)
self.register[patid] = patient
return self.enqueuePatient(patid)

def enqueuePatient(self, PatId):
""" Add patient node to max heap.
Return patient node.
"""

patient = self.register[PatId]
return self._heap_add(patient)

def nextPatient(self):
""" Remove next patient from the heap.
Return deleted patient node (or None).
"""

if self.root is not None:
# dequeue root and heapify the tree again.
return self._dequeuePatient()
else:
return None

def _dequeuePatient(self):
""" Remove next patient from the heap.
Argument: patId (unused, as we do not remove arbitrary patient node
but always the one from the heap's root.)
Argument kept only for compatibility with the question format.
Return deleted patient node.
"""
return self._heap_remove()

def new_patient_banner(self, p):
""" Generate 'New Patient' message.
Return info about the new patient.
"""

return """---- new patient entered ---------------
Patient details: {}, {}, {}
Refreshed queue:
{}
----------------------------------------------
""".format(p.name, p.age, p.PatId, self._heap_items().rstrip())

def _generate_pat_id(self):
""" Generate patient id in <xxxx> form.
Return Patient Id.
"""

self.pid += 1
# patId is like xxxx (eg. 0001)
patid = str(self.pid).rjust(4, '0')
return patid

def _heap_add(self, node):
""" Add a node to max heap tree and heapify the tree. """

self.queue.append(node)
# if heap is empty, add root node and return.
if self.root is None:
self.root = node
return node

# if heap is not-empty, find the (expected) parent of the new node.
parent = self.queue[len(self.queue) // 2 - 1]

# connect the new node to parent's left/right, whichever available.
if parent.left is None:
parent.left = node
else:
parent.right = node

# starting from this node, heapify upwards.
return self._heapify_bottom_up(node)

def _heap_remove(self):
""" Remove the root node from max heap tree and heapify the tree.
Return the deleted (root) node.
"""

# if there are no more elements to delete
if len(self.queue) == 0:
return None

# else, swap root with last node, heapify, and then pop/return last node.

# before swapping, remove parent->last_node pointer.
last_node = self.queue[-1]
parent = self.queue[len(self.queue) // 2 - 1]
if parent.left is last_node:
parent.left = None
else:
parent.right = None

_swap(self.root, last_node)
root = self.queue.pop(-1)

# Tree can be empty here.
if len(self.queue) == 0:
self.root = None
else:
self._heapify_top_down()

return root

def _heapify_bottom_up(self, node):
""" Helper function to heapify the tree from bottom to top.
Return the original node.
"""

parent_pos = len(self.queue) // 2 - 1
parent = self.queue[parent_pos]

while parent is not None and parent.age < node.age:
_swap(parent, node)
node = parent # move up and compare again

# calculate current node's parent's index, special handling for root.
parent_pos = (parent_pos-1) // 2
if parent_pos < 0:
parent_pos = 0
parent = self.queue[parent_pos]

return node

def _heapify_top_down(self):
""" Helper function to heapify the tree from top to bottom.
Return the (new) root node.
"""

if self.root is None:
return

node = self.root
while node is not None:
child = _max(node.left, node.right)
# if current node's age value is smaller than one of it's child,
# swap with larger child.
if child is not None and node.age < child.age:
_swap(node, child)
node = child
else:
break
return self.root

def _heap_items(self):
""" List heap items in sorted order without changing the heap.
- Deep copy the original list.
- Print the max heap as sorted list by removing elements one by one.
- Restore max heap from the copied list.
Return string containing patients info sorted by age.
"""

# deep-copy the original list/heap for later restoration
self.queue2 = copy.deepcopy(self.queue)

output = ""
while len(self.queue) > 0:
node = self._dequeuePatient()
output += "{}, {}\n".format(node.PatId, node.name)

# restore original list/heap
self.queue = self.queue2
self.root = self.queue[0]

return output

def read_in1(self):
""" Read initial input file and register the patients. """

infile = 'inputPS5a.txt'
with open(infile, "r") as f:
for line in f:
# handle 0 or more spaces before/after comma.
if re.match('^.*,', line):
(name, age) = re.split(r' *, *', line.rstrip())
age = int(age)
self.registerPatient(name, age)
return

def write_out1(self):
""" Write the output generated after initial patients are registered. """

outfile = 'outputPS5.txt'
with open(outfile, "w") as f:
text = """---- initial queue ---------------
No of patients added: {}
Refreshed queue:
{}
----------------------------------------------
""".format(self.pid - self.initial_pid, self._heap_items().rstrip())
f.write(text)
return


def main():
# create the initial queue from infile1
cq = ConsultQueue()
cq.read_in1()

# write output to outfile1
cq.write_out1()

# enqueue new patients from infile2.
for line in read_in2():
# we expect either a 'New patient' with name/age info
# or the 'Next Patient' command
if re.match('^newPatient:', line):
# handle 0 or more spaces before/after comma.
(_, name_age) = re.split(r'newPatient: *', line.rstrip())
(name, age) = re.split(r', *', name_age.rstrip())
age = int(age)

patient = cq.registerPatient(name, age)
write_out2(cq.new_patient_banner(patient))
elif re.match('^nextPatient', line):
patient = cq.nextPatient()
write_out2(next_patient_banner(patient))


main()
```

### inputPS6a.txt:

***********************************************************************************************************************************

```
Surya, 60
Ajay, 14
Rishi, 27
```

### inputPS6b.txt:

**********************************************************************************************************************************

```
newPatient: John, 55
nextPatient
newPatient: Pradeep, 45
nextPatient
nextPatient
newPatient: Sandeep, 60
nextPatient
```

### outputPS6.txt

************************************************************************************************************************************

```
---- initial queue ---------------
No of patients added: 3
Refreshed queue:
100160, Surya
100327, Rishi
100214, Ajay
----------------------------------------------
---- new patient entered ---------------
Patient details: John, 55, 100455
Refreshed queue:
100160, Surya
100455, John
100327, Rishi
100214, Ajay
----------------------------------------------
---- next patient ---------------
Next patient for consultation is: 100160, Surya
----------------------------------------------
---- new patient entered ---------------
Patient details: Pradeep, 45, 100545
Refreshed queue:
100455, John
100545, Pradeep
100327, Rishi
100214, Ajay
----------------------------------------------
---- next patient ---------------
Next patient for consultation is: 100455, John
----------------------------------------------
---- next patient ---------------
Next patient for consultation is: 100545, Pradeep
----------------------------------------------
---- new patient entered ---------------
Patient details: Sandeep, 60, 100660
Refreshed queue:
100660, Sandeep
100327, Rishi
100214, Ajay
----------------------------------------------
---- next patient ---------------
Next patient for consultation is: 100660, Sandeep
----------------------------------------------
```

### analysisPS6.txt:

************************************************************************************************************************************

## Analysis of Assignment
========================

## Program logic
### Populating Initial ConsultQueue
--------------------------------

The programs implements a priority queue via a max-heap tree, which is
built one node at a time with the given initial list of patients. The
tree is heapified using the bottom-up approach, each time a patient node
is inserted.

The max-heap is implemented with a python list, which makes it easier to
reach to any node's parent using its index. The list also allows for
arbitrarily large number of nodes to be inserted, the upper bound on the
number of nodes is limited only by system's available memory.


### Refreshing the Queue
--------------------

Once the heap tree is populated with the given list of initial patients,
the queue is refreshed, which means the heap tree is printed in
non-increasing order of patient's age. Printing a heap tree requires
that the elements of the tree are removed one by one, with max-heap
being heapified after every deletion. The deletion uses the strategy of
swapping the last node with heap tree's root (patient node with highest
age), and then heapifying the tree using top-down heapify approach.
The original root node is removed from the tree (python list) and the
process is repeated till the queue is empty.

Since the printing of sorted ConsultQueue requires emptying out of the
original queue, we need to keep a copy of the ConsultQueue for later
restoration of the heap-tree, so that the tree can be refreshed /
printed again, once a new patient is registered.


### Patient Registration
--------------------

Every time a new patient is added to the ConsultQueue, the heap-tree is
heapified using the bottom-up heapify approach.


### Next Patient
------------

A nextPatient command deletes the patient node from the root of the heap
tree using top-down heapify approach.

## Time complexity
### Building initial ConsultQueue
-----------------------------

Initially, if the number of patients having arrived at clinic is 'm' the
time complexity to build the initial ConsultQueue is:

O(m * log m)

Upon building the initial ConsultQueue, it needs to be refreshed / printed
*one time*, incurring an additional:

O(m * log m) complexity.


### Subsequent New Patients
-----------------------

If there are 'n' newPatient commands ('n' new patient arrive
subsequently) while none of the original 'm' patients are removed from
the priority queue, the total size of the max-heap grows to n + m. The
time complexity of insertion for 'n' new nodes is:

O(n * log (m+n))


### ConsultQueue refresh
--------------------

However, as the ConsultQueue needs to be refreshed and restored after
each new patient node is inserted, the complexity for refreshing
ConsultQueue *once* is:

Time complexity of sorting (m+n) elements + Time complexity of backing
up original queue + Time complexity of restoring the queue.

= O((m+n) * log(m+n)) + O(m+n) + O(1) = O((m+n) *
log(m+n))

For 'n' newPatient commands, the complexity becomes: O(n* (m+n) *
log(m+n))


### Next Patient
------------

A patient node is deleted, and tree is heapified.

The heapification is done in: O (log (m+n)) time, assuming the total
queue size is (m+n).

If there are 'p' nextPatient commands, the complexity of deleting 'p'
nodes and heapifying the tree becomes:

O(p * log(m+n))

nextPatient command does not require the queue to be printed, so no
additional complexity is incurred.

### Total Time Complexity
---------------------

The total time complexity can be obtained by summing up all the
individual time complexities above:

2*O(m * log m) + O(n * (m+n) * log(m+n)) + O(p * log(m+n))

with m, n and p being arbitrarily large numbers approaching N, the
upper-bound for the total time complexity can be given by:

O(N^2 * log(N))

## Space complexity

The program uses the following structures to store / implement the max
heap tree as a priority queue.

queue - A python list structure that stores the max-heap tree.

Space complexity incurred by 'queue' structure is:

O(m+n)
here, 'm' being the count of initial patients, and 'n'
patients are added subsequently.


queue2 - Another python list structure to back up the 'queue' contents
before refreshing, and restore the original heap tree subsequently.

Space complexity incurred by 'queue2' structure is also:

O(m+n)


register - A python dict structure to map the patient id to patient
nodes. This one is *not* required if we choose to pass patient info
using PatientRecord node, instead of patient id. However, as the
skeleton program of problem expects to pass patient-id to
_enqueuePatient instead of PatientRecord, we need a mapping
structure to get the correct PatientRecord node.

Space complexity incurred by 'register' structure is also:

O(m+n)

## Total space Complexity
----------------------

The total space complexity can be obtained by summing up all the
individual space complexities above:

3 * O(m + n) = O(m + n)

which can be considered as

O(N)
N being the total number of the patients.


## Further Optimization and Takeaways

- A max heap tree is not a suitable structure where one needs to print
the sorted list frequently. As the full sorted list can only be obtained
after removing all elements one by one, this incurs O(n*logn)
complexity for every print operation.
A structure such as a binary search tree is a better fit in such cases,
which can provide a sorted list in O(n) time, thus reducing the total
time complexity for 'm' sorted-print operations to
O(mn) instead of the current O(mn logn).

- max heap can be built in O(n) time complexity when all the initial n
nodes are given. This approach uses only non-leaf nodes for
heapification, starting from the lowest level of the initial level-order
tree.
The current implementation builds the tree one element at a time,
and incurs O(n logn) for heap building.
This can be improved.

- An ideal solution to the given problem would be by making use of an
*additional* binary search tree for printing the sorted list. This comes
at the cost of an additional O(n) space complexity.

In this case -

* Each new node would be added to both the heap tree and BST with
O(logn) time complexity.

* A deletion would cause the node to be deleted from both heap and
BST with O(logn) time complexity.

* Printing a list would print the sorted list by traversing BST only,
with O(n) time complexity, thus 'm' print operations would require O(mn)
complexity.

* Additionally, we would not require a backup queue to preserve original
heap tree, as the sorted print happens only through BST; thereby
canceling out the added space complexity of maintaining a BST.