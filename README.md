# Data-structures-and-Algorithm
The repository is based on University of Toronto CSC263 to analyze a variety of data structures.
## Augmented Data Structure
Assume we already know a variety of data structures, such as stack, queue, binary search tree, avl tree, heap...\
Augmented data structure modify an existing data structure to store additional information and perform additional operations.
### There are four steps to define a augmented data structure.
1. Decide what base data structure to use.
  We need to define what base data strucuture, because the new data structure has same operations with data structure that we learned.\
  Therefore, the base data structure decide the base operations in the new data structure.
2. Specify additional information.
  When we add more variables/information to the new data strucutre, the new data structure can call more information dierctly, which is similair to
  that the each element in new data structure has a new pointers to point the new information.
3. Specify additional operations.
  We might need to add new operations or some help functions in order to store the more information.
4. Adjust odd operations.
  When each element stored more information in the new data structure, the information needs to update with the opeartions
  Therefore, we need to modify or add the new information update based on original data structure operations.
