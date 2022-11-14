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
### Augemented a AVL tree by Binary Search tree.
1. we decide to use BST to implement the AVL tree.
2. what additional information and operations ?
- height(Tree.node)(avl tree needs to caculate the balance factor for each nodes)
- rebalance(Tree.node)(each node rotates with each others, and it should follow the avl priority)
- rotate(Tree.node)
- insert/delete(Tree.node) (each node hight needs to maintain in the two operations.)
### Augemented a Orderset by AVL tree
1. we decide to use AVL tree to implement the Orderset.
2. what additional information and operations ?
- rank(k), input a element, return its rank
- select(r), input a rank, return its element
- Example, {27,50,15,9,34,12} rank(34) = 5, select(3) =5
#### First attmept without any addition of information
![avl image](/image/image1.png)