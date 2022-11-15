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
  - `height(Tree.node)`(avl tree needs to caculate the balance factor for each nodes)
  - `rebalance(Tree.node)`(each node rotates with each others, and it should follow the avl priority)
  - `rotate(Tree.node)`
  - `insert/delete(Tree.node)` (each node hight needs to maintain in the two operations.)
### Augemented a Orderset by AVL tree
1. we decide to use AVL tree to implement the Orderset.
2. what additional information and operations ?
  - `rank(k)`, input a element, return its rank
  - `select(r)`, input a rank, return its element
  - Example, {27,50,15,9,34,12} 
  
    rank(34) = 5,
  
    select(3) =5
#### First attmept without any addition of information
![avl image](/image/image1.png)

`rank(30) = 4`

`select(8) = 38`

Since this is avl tree, search/insert/delete $\in \theta(logn)$.
1. `rank(k)`: we need to find how many elements are less than the k.
Therefore, the avl tree will traversal elements that less than k to arrive the k, the rank(k) $\in \theta(n)$
2. `select(r)`: we need to find how $r_{th}$ largest element.
Therefore, the avl tree will traversal r-1 elements to arrive the $r_{th}$ largest elemet, the select(r) $\in \theta(n)$
#### The Optimize for first attempt
1. The rank serve as the additional information for each node
2. ![avl image with rank](/image/image2.png)
3. When we store the rank for each nodes, it is similar to build a new avl tree inside original avl tree.
4. Therefore, `select(r)` is same with the basic avl search operation, its time complexity $\in \theta(logn)$.
5. `rank(k)` just call one `select(r)`, its time complexity $\in \theta(logn)$.
6. `insert/delete` update the rank.
#### Third attempt with storing subtree size for each node.
![avl image with count](/image/image3.png)

## Hash 
All algorithm in the world is for processing data more efficiently. There are two kind of efficiency in the computer algorithm, and they are
Time complexity and Space complexity. Before this section, we pursued the efficiency in the time complexity but not combined the space complexity.
In order to the extreme time complexity, we must sacrifice the space complexity to trade in time complexity.

### Direct-address tables
What the meaning of "direct" in computer science? Easy way? Direct way?
The direct-address tables is a direct way to store data without any optimization.
For example, when we need to implement an ADT dictionary by the direct-address tables, we just store all
data that we need in the set with unique key for each element. The `insert`,`delete`,`search` $\in O(1)$, but the direct-address tables occupy huge space,
which is not practical for implement when the number of elements is huge.

### HashTable
According to the direct-address tables, we can not guarantee that each data has unique key or the set of possible keys are small.
Therefore, we need to optimize the direct-address tables as hash table, which makes the way that stores data generally.
HashTable has "slot" or "bucket" as the space for each data, and a Hash function to produce the correspond key for each element.
`Search(k)` -> find T[h(k)]

`Insert(X)` -> Insert X.k into the T[h(X.key)]

`Delete(X)` -> Remove X from T[h(X.key)]

However, the |U| > the number of slots, which will lead to that one slot occupy more element, although they have same key.
Therefore, there are two different addressing for the collision, open addressing and closed addressing.

#### Closed addressing
![hash](/image/image4.png)
When the hash function produce the key, there are collisions  in closed addressing, we use the Doubly Linklist to connect each key.

Worst Case

`insert(x)`

    -search x.key
    -either replace or add x 
    -$\in O(1)$

`delete(x)`
    
    -search x.key
    -remove node
    -$\in O(1)$

`search(x)`
![hash](/image/image5.png)

    -When there is so trash hash function, plug all key in one slot
    -$\in O(n)$