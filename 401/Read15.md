# Trees

## Terminology

* Node - A Tree node is a component which may contain it’s own values, and references to other nodes.
* Root - The root is the node at the beginning of the tree.
* K - A number that specifies the maximum number of children any node may have in a k-ary tree. In a binary tree, k = 2.
* Left - A reference to one child node, in a binary tree.
* Right - A reference to the other child node, in a binary tree.
* Edge - The edge in a tree is the link between a parent and child node.
* Leaf - A leaf is a node that does not have any children.
* Height - The height of a tree is the number of edges from the root to the furthest leaf.

## Traversals

An important aspect of trees is how to traverse them. Traversing a tree allows us to search for a node, print out the contents of a tree, and much more! There are two categories of traversals when it comes to trees:

### Depth first

Here we go through the depth of the tree first, there are three methods for that:

* Pre-order: `root>>left>>right`

* In-order: `left>>root>>right`

* Post-order: `left>>right>>root`

![depth](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-15/resources/images/tree-example.png)

according to the previous tree, the traversal would result in the following paths:

* Pre-order: A, B, D, E, C, F

* In -order: D, B, E, A, F, C

* Post-order: D, E, B, F, C, A

The best way to traverse through tree is to use **recursion**.

#### Pre-order

```shell
ALGORITHM preOrder(root)

OUTPUT <-- root.value

if root.left is not NULL
    preOrder(root.left)

if root.right is not NULL
    preOrder(root.right)

```

### Traversal pseudo-code

#### Pre-order

```shell
ALGORITHM prALGORITHM postOrder(root)
// INPUT <-- root node
// OUTPUT <-- post-order output of tree node's values

    if root.left is not NULL
        postOrder(root.left)

    if root.right is not NULL
        postOrder(root.right)

    OUTPUT <-- root.value
eOrder(root)
// INPUT <-- root node
// OUTPUT <-- pre-order output of tree node's values

OUTPUT <-- root.value

if root.left is not Null
    preOrder(root.left)

if root.right is not NULL
    preOrder(root.right)
```

#### In-order:

```shell
ALGORITHM inOrder(root)
// INPUT <-- root node
// OUTPUT <-- in-order output of tree node's values

if root.left is not NULL
    inOrder(root.left)

OUTPUT <-- root.value

if root.right is not NULL
    inOrder(root.right)
```

#### Post-oeder


```shell
ALGORITHM postOrder(root)
// INPUT <-- root node
// OUTPUT <-- post-order output of tree node's values

    if root.left is not NULL
        postOrder(root.left)

    if root.right is not NULL
    postOrder(root.right)

OUTPUT <-- root.value
```

### Breadth first

Breadth first traversal iterates through the tree by going through each level of the tree node-by-node.

![Breadth](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-15/resources/images/tree-example.png)

Output: `A, B, C, D, E, F`

#### Pseudo-code

```shell
ALGORITHM breadthFirst(root)
// INPUT  <-- root node
// OUTPUT <-- front node of queue to console

Queue breadth <-- new Queue()
breadth.enqueue(root)

while breadth.peek()
node front = breadth.dequeue()
OUTPUT <-- front.value

if front.left is not NULL
    breadth.enqueue(front.left)

if front.right is not NULL
    breadth.enqueue(front.right)
```

## K=ary Trees

```shell
ALGORITHM breadthFirst(root)
// INPUT  <-- root node
// OUTPUT <-- front node of queue to console

Queue breadth <-- new Queue()
breadth.enqueue(root)

while breadth.peek()
node front = breadth.dequeue()
OUTPUT <-- front.value

for child in front.children
    breadth.enqueue(child)
```

### Big O

* The Big O time complexity for inserting a new node is O(n). Searching for a specific node will also be O(n).

* The Big O space complexity for a node insertion using breadth first insertion will be O(w), where w is the largest width of the tree.
