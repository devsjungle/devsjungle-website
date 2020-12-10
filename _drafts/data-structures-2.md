Doubly linked lists

Stacks
Queues

<!-- Attention Grabbing Intro! -->


<!-- Subheaders! -->

## Stacks
Stacks are very simple in their nature, but they can be used to solve harder problems using them. That's why they are super common during interviews. They are quite literally a stack of data, much like a stack of anything (books, money, pancakes) if we can only handle one element at a time it's always the topmost element in the stack. Either we add another pancake to our stack or we remove the first one from it. That's the idea behind them.

### How do they work?
Internally it's rare to see a data structure that is only a stack. But a lot of them can be used as a stack in a given situation. Let me illustrate with an example.

```python
money_stack = [100, 100, 100, 50, 100]
money_stack.pop()
money_stack.pop()
money_stack.append(100)
```
```javascript
var money_stack = [100, 100, 100, 50, 100]
money_stack.pop()
money_stack.pop()
money_stack.append(100)
```
Here we used both arrays from 2 different languages as stacks! Even though they have very different ways of doing things under the hood!

### Time Complexity
The traditional operations don't make much sense when talking about stacks. Since the usability is so straight forward and limited the operations time complexity are also simple to reason with. The main topic I will show you are the common uses and interview questions they may show up on.
 
#### Operations

- Access: In a stack it's not common for us to go to anywhere beyond the topmost item. But since it's uncommon for us to have a pure stack data structure as I showed above, you can access elements below the first one, but that time complexity will depend on the language you are using, not because of the way you are using it.
- Search: Again same idea from accessing, we don't really search for things inside a stack, we just look at the topmost element from the stack!
- Insertion: Putting an item in a stack is quick and easy, in the real world if the stack is too big (imagine a mountain of money) it may be hard to put another element on top of it, but in a computer it doesn't matter the size of our stack, the time it takes to add a new element is always the same, which means constant time or O(1)!
- Deletion: Removing an item costs the same as inserting it, no matter its size! Also constant time O(1). 

### Common uses:


### Common Stacks Interview Questions
### How it works on other languages?


## Queues
 
### How do they work?
### Time Complexity
 
#### Access
#### Search
#### Insertion
#### Deletion
 
### Common Queues Interview Questions
### How it works on other languages?
