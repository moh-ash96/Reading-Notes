# Stacks and Queues

## Stack

A stack is a data structure that consists of **Nodes**. Each **Node** references the next Node in the stack, but doesn't reference its previous.

### Terminology

1. *Push*, Add nodes to stack.

2. *Pop*, Remove nodes from stack, and when the stack is empty, using pop will raise an exception.

3. *Top*, The top of the stack.

4. *Peek*, View the value of the top node, and when stack is empty, using peek will raise an exception.

5. *IsEmpty*, returns True if the stack is empty.

### Stack flow concepts

#### FILO

**F**isrt **I**n **L**ast **O**ut, which means the first item added to the stack will be the last item popped out of it.

#### LIFO

**L**ast **I**n **F**irst **O**ut, The last item added to the stack will be the first item popped out.

### Visualization

![stack](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/stack1.PNG)

#### Push O(1)

Pushing a node into the stack is always **O(1)** operation.

##### Steps

1. First, you should have the Node to add.
![1st-step](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/pushStack1.PNG)

2. Assign the **next** property of **Node 5** to reference the same Node that **top** is references.
![2nd-step](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/pushStack2.PNG)

3. Reassign the reference **top** to the newly added Node.
![3rd](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/pushStack3.PNG)

##### pseudo code

```shell
ALGORITHM push(value)
//INPUT<-- value to add, wrapped in Node internally
//OUTPUT<-- none
    node = newNode(value)
    node.next<--Top
    top<-- Node
```

#### Pop O(1)

Removes a node from the top.
![pop](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/popStack1.PNG)

##### Steps

1. Create a reference called *temp* that points to the same Node that  
    *top* points to.

  ![1st](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/popStack2.PNG)
2. Re-assign top to the value that the next property is referencing.
    In our visual, we can see that the next property is pointing to Node 4.
    ![2nd](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/popStack3.PNG)
3. Clear next property from current temp reference.
    ![3rd](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/popStack4.PNG)
4. return value of current.

##### pseudo code

```shell
ALGORITHM pop()
// INPUT <-- No input
// OUTPUT <-- value of top Node in stack
// EXCEPTION if stack is empty

   Node temp <-- top
   top <-- top.next
   temp.next <-- null
   return temp.value
```

#### Peek

```shell

ALGORITHM peek()
// INPUT <-- none
// OUTPUT <-- value of top Node in stack
// EXCEPTION if stack is empty

   return top.value
```

#### IsEmpty

```shell

ALGORITHM isEmpty()
// INPUT <-- none
// OUTPUT <-- boolean

return top = NULL
```

## Queue

### Terminology


1. Enqueue - Nodes or items that are added to the queue.
2. Dequeue - Nodes or items that are removed from the queue. If called.
3. when the queue is empty an exception will be raised.
4. Front - This is the front/first Node of the queue.
5. Rear - This is the rear/last Node of the queue.
6. Peek - When you peek you will view the value of the front Node in
7. the queue. If called when the queue is empty an exception will be raised.
8. IsEmpty - returns true when queue is empty otherwise returns false.

### Concepts

FIFO
First In First Out

This means that the first item in the queue will be the first item out of the queue.

LILO
Last In Last Out

This means that the last item in the queue will be the last item out of the queue.

### Visualization

![queue](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Queue.PNG)

#### Enqueue O(1)

![enqueue](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Enqueue1.PNG)

* Step1

![1](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Enqueue1.PNG)

* Step 2

![2](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Enqueue3.PNG)

* Step 3

![3](https://codefellows.github.io/common_curriculum/data_structures_and_algorithms/Code_401/class-10/resources/images/Dequeue3.PNG)

##### pseudo-code

```shell
ALGORITHM dequeue()
// INPUT <-- none
// OUTPUT <-- value of the removed Node
// EXCEPTION if queue is empty

   Node temp <-- front
   front <-- front.next
   temp.next <-- null

   return temp.value
```

#### Peek O(1)

##### pseudo-code

```shell
![](ALGORITHM peek()
// INPUT <-- none
// OUTPUT <-- value of the front Node in Queue
// EXCEPTION if Queue is empty

   return front.value)
```

#### IsEmpty O(1)

##### pseudo-code

```shell
ALGORITHM isEmpty()
// INPUT <-- none
// OUTPUT <-- boolean

return front = NULL
```
