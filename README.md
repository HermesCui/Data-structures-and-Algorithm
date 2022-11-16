# Data-structures-and-Algorithm
The repository is based on University of Toronto CSC263 to analyze a variety of data structures.
## Augmented Data Structure
Assume we already know a variety of data structures, such as stack, queue, binary search tree, avl tree, heap...\
Augmented data structure modify an existing data structure to store additional information and perform additional operations.
### There are four steps to define an augmented data structure.
1. Decide what base data structure to use.
  We need to define what base data structure, because the new data structure has same operations with data structure that we learned.\
  Therefore, the base data structure decide the base operations in the new data structure.
2. Specify additional information.
  When we add more variables/information to the new data structure, the new data structure can call more information directly, which is similar to
  that each element in new data structure has a new pointers to point the new information.
3. Specify additional operations.
  We might need to add new operations or some help functions in order to store the more information.
4. Adjust odd operations.
  When each element stored more information in the new data structure, the information needs to update with the operations
  Therefore, we need to modify or add the new information update based on original data structure operations.
### Augmented an AVL tree by Binary Search tree.
1. we decide to use BST to implement the AVL tree.
2. what additional information and operations ?
  - `height(Tree.node)`(avl tree needs to calculate the balance factor for each node)
  - `rebalance(Tree.node)`(each node rotates with each others, and it should follow the avl priority)
  - `rotate(Tree.node)`
  - `insert/delete(Tree.node)` (each node height needs to maintain in the two operations.)
### Augmented an Order set by AVL tree
1. we decide to use AVL tree to implement the Orderset.
2. what additional information and operations ?
  - `rank(k)`, input an element, return its rank
  - `select(r)`, input a rank, return its element
  - Example, {27,50,15,9,34,12} 
  
    rank(34) = 5,
  
    select(3) =5
#### First attempt without any addition of information
![avl image](/image/image1.png)

`rank(30) = 4`

`select(8) = 38`

Since this is avl tree, search/insert/delete $\in \theta(logn)$.
1. `rank(k)`: we need to find how many elements are less than the k.
Therefore, the avl tree will traversal elements that less than k to arrive the k, the rank(k) $\in \theta(n)$
2. `select(r)`: we need to find how $r_{th}$ largest element.
Therefore, the avl tree will traversal r-1 elements to arrive the $r_{th}$ largest element, the select(r) $\in \theta(n)$
#### The Optimize for first attempt
1. The rank serve as the additional information for each node
2. ![avl image with rank](/image/image2.png)
3. When we store the rank for each node, it is similar to build a new avl tree inside original avl tree.
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
    -O(1)

`delete(x)`
    
    -search x.key
    -remove node
    -O(1)

![hash](/image/image5.png)

`search(x)`

    -When there is bad hash function, plug all key in one slot
    -O(n)

Let the m is the number of slots, and n are the number of keys that we need to plug in
n/m is the load factor in the HashTable.\
Assume we have a perfect hash function so that each node are uniform distribute in the HashTable.\
when m > n, the average time complexity of `search(x)` $\in O(1)$. 

We can explain it informal:\
When m > n, which represents our has slots enough to store each node, and each will average distribute in the table. Hence, 
the table must be not occupy fully and each slot only has one node.
Therefore, the average time complexity of `search(x)` $\in O(1)$.\
(If you would like to see the formal proof for the average time complexity of search, check CLRS chapter 11.3)
#### Open addressing
When there is collision,the strategy examine buckets one by one. If one slot is occupied, it will plug in the node into next slot.\
This process called probe. Besides, there are three ways to probe.\
1. Linear probing\
    let H(k) is the original has function.\
`H'(k,i) = (H(k) + i)%m`, i from 0 to n\
However, the linear probing will produce the clusters in the HashTable, it will waste the space.
Therefore, the quadratic probing will optimize it.
2. Quadratic probing\
   `H'(k,i) = (H(k) + ai + bi^2)%m`, i from 0 to n\
However, there is special case to produce clusters.
3. Double Hash\
   `H'(k,i) = (H1(k) +H2(k))%m`
   We use two hash function to prob each key, which can randomly separate each node.

`Insert`

    -search x.key
    -either replace or add x
    - O(1)

`delete(x)`
    
    -search x.key
    -remove node
    - O(1)

`search(x)`
![hash](/image/image6.png)

    -When there is bad hash function, plug all key in one slot
    -O(n)
   When h(k1) = h(k2) = h(kn) and we would like to search the kn, we need to call h(kn). Then the search will check the key from 1 to m-1, which leads to that the time complexity is O(n).

##  QuickSort
QuickSort is often the best practical choice for sorting because it is efficient and stable time complexity on the average thoguth its worst-case running time O(n^2) on an input array of n numbers.

There three steps to implement the quicksort.

Divide: We will pick a pivot as the divider of quicksort, the pivot is q in the A[p...q...r]. Then the A will be seprate to A[p..q-1] and A[q+1..r] such that all elements in A[p..q-1]are less than A[q] and all elements in A[q+1..r] are greater than A[q].

Conquer: Sort the two subarrays A[p..q-1] and A[q+1..r] by the resursive method.

Combine: just add the two sub array together, and the A[p..r] is sorted.

### Performance of quicksort

The partitioning plays a significant role in the running time performance. If the partitioning is balanced, the runing time will be asymptotically as fast as O(nlogn). If the partitioning is unbalanced, the runing time will be asymptotically as fast as O(n^2).

In the worstcase (informal explaining), each partition splits one element each recusion, the whole array will partition n times with each partition $\in O(n)$.

Therefore the time complexity of whole process will be O(n^2).

In the bestcase(informal explaining), the partition will split the array into two balanced subarray by each recusion. Therefore, each the recusion will run at least O(logn) times with each partition O(n). The whole process will be O(nlogn).

### A randomized version of quicksort 

In order to reduce the probability of worst case in the quicksort in order to obtain good average performance.

Therefore, there is a randomization technique, called random sampling. We will randomly chose element as the pivot.

### Performance of randomized version of quicksort

In the worst case, the probability of worst case in the quicksort is reduced, but it still exist the probaility of worst case in the randomized quicksort. Therefore, the running time will be O(n^2).

In the best case, it is same with normal quicksort O(nlogn)

In the average case, since, the probability of worst case approach 0, the average running time is O(nlogn).