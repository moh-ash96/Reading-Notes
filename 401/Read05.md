# Linked lists

A linked list is a sequence of *nodes* that are connected to each other and each node references the next node in the link.

## Terms

* **Data structures**, they are the different ways that we can organize our data;*variables, arrays,hashed,and objects*

* **linear data structure**, data that has a sequence and order to how it is constructed and traversed.

* **Linked list**, it as data structure contains nodes that points to the next node in the list, we can assume them as arrays, because there are pretty much similarity between the two.

* **Singly**, it refers to the number of reference points to the next node in the linked list.

* **Doubly**, it refers to their being two references within a node, *Next*, and *previous*.

* **Circular linked list**, a list that it's end doesn't point to a null value, instead it points to the head.

* **Node**, Individual items that are in a linked list, each node contains the data for each link.

* **Next**, refers to the next node.

* **Head**, refers to the first node in the linked list, and it is the only entry point of the list.

* **end**, it's the last part of the list and it always refers to null.

* **Current**, refers to the node that is being looked at.

### The diffidence between arrays and linked lists

When array is created, it needs a certain amount of memory in one contiguous block, while linked lists need certain amount of memory but they are scattered all over the memory, it is possible for one byte to live somewhere in the memory and the next one is stored in another place.

## What dows it look like

![linked list](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-05/resources/images/LinkedList1.PNG)

### Transversal

In order to traverse over a linked list we shall use a *while* loop and set its condition as `if not null` because we want the traversing to start from the beginning because as we said the only link referencing to null is the last one.
So the first step is to create a current at the head, then we create the while loop to keep moving over the node and checking as long as the current node doesn't refer to null i.e. **not the end of the list** so if the value we are looking for is not in the current node, it will move to the next one, until it finds the value, and here it will return *true*, or it will refer to null, here the loop will stop and the app will crash.

The Transversal Big O is 

* **O(n)** in time because at worst case it will take the time of **n** which represents the last node in the list.

* **O(1)** in space, because no additional space is being used more the space already given by the input.

### Adding Node

#### Adding O(1)

When we want to add a node as O(1), we should add it at the beginning of the list, which means, we should replace the head without loosing the reference to the next node.
So we start by making an add function giving it an argument of the value we want to add, in default settings, the newNode.next should be null, bet we need to change it to be in place of the head i.e. referring to the next node, the head will be reassigned to refer to the new node.
Here the Big O for time and space are O(1),because it doesn't matter how many nodes we add it takes the same time and space as the input at each step.

#### Adding O(n)

Here we need to add a node in the middle of a list, so we can either use add before or add after, in this case we are using add before.
We will start by creating a new node giving it a specific value, and by default its next will be null, the we target the value of the node we want to add the new one before, after that, we traverse over the link list using while loop setting the condition as *next doesn't equal null* so the traverse will go through the whole list until it reaches the value to put new node before, when the value is reached we will set the newNode.next to be that value, but here there are two values referring to the same node so because the current is pointing at the sme node that the node before is, we change the direction of the current.next to be at the value of the new node, and thats it.
Big O:

* **O(n)**, for the time because at worst case it will go through the list to the node number of *n*.

* **O(1)**, for the space, because we are not adding any new space.

### Printing the Node

Here we will use the while loop, setting the condition to current is not null, so we don't reach the end of the list and before the while loop restarts, we set the current as current.next, to go to the next node, while we are printing on the way.
When the end is reached we write out the *null* pointed to by the last node.

## Big O Notation

It is a way of evaluating the performance of an algorithm, by putting under consideration how much time it requires at runtime given how much time and memory it needs.

### Types of Big O Notations

![Big O](https://miro.medium.com/max/500/1*FC0XX0-9Vx7yCS0dTS2Zrw.jpeg)

* O(1) function, it takes constant time, which is to say that it doesn't matter how many elements we have or how huge is the input is, it'll always take the same amount of time and memory to run our algorithm.

* O(n) function, it is linear, which means that as our input grows, the space and time that we need to run that algorithm grows linearly.

* O(n^2) function, it takes exponentially more time and memory the more elements that you have.
