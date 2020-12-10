
<!-- # Data Structures and Algorithms to leverage your seniority - Part 1 -->
# Knowing these data structures will make you more senior software developer [Part 1]

## Intro

Something I stumble upon very often are thirsty software developers, traveling the corporate jungle, lost, confused with no idea where to go to. I know I have felt like this numerous times. Specially when it came to leveling up my skills going from a Junior/Middle into a Senior level. Heck! I am still learning a lot about it and although there are several aspects to it, when it comes to hard skills, data structures and algorithms are undoubtedly the fundamental building blocks we work with every single day. 
Understanding these at a fundamental level will boost your chances of making better and more impactful decisions as a software developer, not to mention the job offers you may get. A sentence a teacher of mine said a long time ago was "The more you study, the luckier you will be" that's exactly how I felt after getting my last job. I kept saying I was lucky of knowing about data structures (which was 90% of the final test), but I had been studying hard for it for some time. The coolest thing is that this knowledge can be applied for any programming language! By the end of this post you should have learned:
 - what are these data structures?
 - most common types
 - what they eat? how they work?
 - whats the 80/20 around data structures.

I will do it by showing practical *modern* examples for each example we go through! One last thing before we begin, this tutorial is not recommended for complete beginners to programming. With all that being said time let's learn how to travel this jungle!

## What and why data structures and algorithms?
Very rarely we work with single data values, specially nowadays where we are generating and collecting more and more data by the day. We need to have a way to store all this data. Having different data structures help us deal with this data more efficiently depending on our situation. What about algorithms? any kind of algorithm? not exactly, when you see data structures and algorithms, the latter refers to algorithms regarding the former.

You may be asking, "But nowadays we gotta learn about these new frameworks and libraries, there are so many of them, I don't have time to learn this, there are more important things to know about!". It's exactly because they are so many that you should learn this, frameworks and libs come and go, but these fundamental data structures exist since the beginning and they will keep on being used for a long time. Not even quantum computing will take these bad boys out. 

Today we will see two data structures Static Arrays and Linked Lists They will serve as an intro, understanding them will enable us to go to bigger and even more awesome things in the near future.
*Let's begin!*


# Static Arrays

The first data structure we will tackle are static arrays. These may look like the most common data structure there is, but actually when you do 

```python
array = [] # in python
```
```javascript
var array = [] // in javascript
```
```c
int  array[10]; // in C
```

they are not the same thing under the hood! They all look very similar on a high level, but you will se they make a huge difference when using them. Each different implementation has its pros and cons.


### How do they work?
When we tell the c compiler to do:

```c
// c code below
int array[10]; 
// or
int array[10] = {0, 1, 2, 3, 4, 5, 6, 7};
```

what actually happens inside the computer’s memory is that it takes 10 sequential slots of memory with each slot having the size of int. This way it makes it trivial to access each element of the array with a given index. The array variable holds the address in memory to access the first element and using the syntax array[x], where x is a number from 0 to 9, we can go directly to the space in memory we want. This has its benefits, instant access to any given element, but also its downsides. What happens if we want to add an 11th element? In C you would have to create a new array and it would choose another 11 slots in memory to dedicate it to the new array. In C they have another great benefit, you don't have to deal with the funky pointers! Just because you don't have to doesn't mean you can't though.

### Time Complexity

#### Access 
As told above, since we know exactly how the data is structured in memory, access is constant, it doesn’t depend on the size of the list. It’s basically a sum. Which for us humans may take a while when we have to sum big numbers but for computers it’s easy as pie.

```c
// nth element address = first element address + (n - 1)

array[4];
```

### Search
Let’s think, how do we find the number 6 inside our array? If we know how the array was initialized it’s easy, we know it’s on index 6, so array[6] gets it. Unfortunately that never happens, so we have to search every element in the array with a simple search, something like:

```c
int searched_number = 6;
int array_size = 10;
for(int i = 0 ; i < array_size; i++){
	if(array[i] == searched_number){
		return i;
	}
} 
return -1;
```

You might be confused with the last line returning -1, that is something very common in C programs where you send an agreed upon value considered the value when stuff goes wrong, or simply when a specific case happens, in this case not finding the searched number inside our array.

Finally, what would the cost of this algorithm look like? Well, best case scenario the number we are looking for would be at the first position, worst case scenario the number would not be inside our array, but he would still need to travel the whole array to make sure. If the array has 10 positions it’s practically instant, but what if they are huge, like millions of numbers inside them? that would take a lot more time to process, and this growth is linear to the size of our input (our array). A fancy way of saying this is that the array has O(n) time complexity when performing a search algorithm.

### Insertion

This one is a little trickier, it involves us having to move things around, let’s imagine we want to insert the number 10 between 3 and 4. 
```c
int array[10] = {0, 1, 2, 3, 4, 5, 6, 7, <empty>, <empty>, <empty>};          
                           #/\ put 10 here
```
well we would have to move numbers 4, 5, 6 and 7 one slot to the side and then put 10 on the 5th position (index 4). Let’s analyze this algorithm:

```c
int index_to_insert = 4;
int number_to_insert = 10;
for(int i = size_of_array - 1; i >= index_to_insert; i--){
    array[i] = array[i-1];
}
array[index_to_insert] = number_to_insert;
```

But this has its limitations, what if the array was full? we wouldn't be able to insert anything without removing another number or creating a new array with enough space for all elements. This is one of the drawbacks for static arrays.

Let's reason again about its time complexity. Best case scenario the number we had to insert would be at the very end, so me would have to do no moving around. Worst case? It would be at the very beginning, having to move all numbers one slot to the side. So here the time complexity would increase linearly as the size of the input (our array) increases. The fancy way of saying it is the time complexity for this operation is O(n).

### Deletion

The same analogy from insertion applies to deletion, we need to move things around after deleting a number. 

```c
// getting from here
array = {0, 1, 2, 3, 4, 5, 6, 7};

//to here
array = {0, 1, 2, 3, 5, 6, 7};
```

As you may guess the code would be very similar to inserting.

```c
int index_to_remove = 4;
for(int i = index_to_insert; i < size_of_array - 1; i++){
    array[i] = array[i+1];
}
```

A few things to notice are:
- we now move from left to right, pulling the next value into the current value.
- we have to stop at size_of_array - 2, because if we go to i = size_of_array - 1 and then do the operation array[i+1] we are accessing the 11th position of an array of size 10. Never a good idea!

Again the time complexity, what is it gonna look like and why? I'll have you figure this one out by yourself. ;)

## Practical Application
<!-- #NOTE: (maybe this should be moved up!) -->

Just to sum things up we saw that static arrays have the following characteristics.
Pros:
- No need to handle pointers (which is good for beginners but also limits your knowledge)
- Accessing a value takes constant time or O(1)

Cons:
- Searching, Inserting or Deleting take linear time O(n), which is not terrible but also not great.
- The size needs to be declared beforehand and it's fixed, you can either run out of memory or you have too much space and left out memory that isn't used.

Looking at these let's think of what would be some good use cases for arrays, where we leverage the pros and nullify or mitigate the cons.

The traditional example of having an array of students and every element would be a student structure. This might be ok, if we only take past students, but if we are constantly adding or removing students each time we do it will cost us time, not only that but we never know how many students will come in each month or year. 

<!-- #IMG of crossword and sales -->

A better use case is if you wanted to make a crossword puzzle and each element contains the letter the person has to guess or something more predictable like the revenue of a company by month. You know every month will have a total revenue, maybe divided by the revenue of each sector of the company.

### Common Static Array Questions
- How arrays work?
- Pros and Cons of an array?
- Can we change the size of an array at run time?
- What are the common operations time complexities?
- How to reverse an array?


### How it works on other languages

Java is very similar to C, the major difference is that when we do:
```Java
int array[10];
```
it allocates that space and fills every slot with a 0 in it. It spends a little more processing, but it may be useful if you weren't planning on filling the slots instantly with something else.

# Linked Lists

Linked lists are one of the most primitive and old data structures created, yet they are still used to this day by most if not all programming languages out there. Many developers use them without knowing the hows and whys behind these minimalistic masterpieces. 

They have a nice contrast with static arrays, they serve a very different purpose as we'll see shortly.

### How do they work?

A linked list is basically a bunch of nodes connected to one another in a sequential manner. Instead of having a sequential space in memory now "random" places in memory are chosen to store our data. "How do I know which element goes before which?" you might ask, in every node of our linked list we have the location of the next node! The structure of a node would have to be implemented by hand using C and it would look something like this:

Disclaimer: for this part you have to know the basics of pointers, we have some resources to guide you here and we are more than happy to explain any questions you might have about them! Recommended resources.

```c
typedef struct n{ // 1
    int value; // 2
    struct n* next; // 3
} NODE; // 4
```

Let's break this down so we get exactly what is happening here, line by line.
1 and 4 - "struct n" this is just the c way of making a new structure and typedef we are creating an alias for our structure, instead of always having to call it using struct n we can simply call it NODE. A more generic typedef could be something like typedef int i; here we are aliasing the int type to i.
2 - is self explanatory...
3 - we declare a variable called next and its type is pointer of struct n. A little confusing but it means we want each node to point to the next node, the node type is struct n  so we get struct n*;

Wait a minute, didn't you just said we could use NODE instead of struct n, why not NODE*? Great question! The statement typedef only ends at line 4, so inside line 3 the aliasing isn't complete, that's why we have to use the verbose name struct n!

Now that we have the basic gist of how linked lists works let's see how they perform!

### Time Complexity

#### Access

Since we don't have the benefits of a sequential space in memory (being able to predict exactly where each slot is), the only place we can find the information for i.e. the last node, is the one before him, and to access that one is the one before him, see where this is going? Let's ilustrate with an example:

# IMG nodes connected.

Here we have 3 nodes, they represent 3 people living together. Mary, John and Griselda, each having contributed 5, 2 and 6 dollars. The value inside each node indicates the amount of times their contributions to the house they live in. If we wanna know what's Griselda's contribution we have to get her address from John's node... And to get John's node address we have to get Mary's address. Since Mary is the first node we have to have it saved somewhere in order to access it, much like we keep an static array first position of the sequence.

Great! Let's quickly check how that would work:

```c
//initializing
NODE* contributions;

int access_index = 2;
NODE* pointer = contributions->next; //?
int counter = 0;

while(pointer != NULL){
    if(counter == access_index){
        return pointer->value;
    }
    counter++;
    p = p->next;
}

return NULL; //?
```

Since we deal with pointers inside our nodes we gotta use the funky point syntax, but it's gonna be fine, trust me. The way we traverse the linked list is with the while statement plus the last line inside the while p = p->next; this is equivalent of doing a for loop and incrementing it at the end, but instead of incrementing the number to have access to the next position we "increment" the node we are in, moving it to the left. 

<!-- # IMG or GIF ilustrating the swap in pointer value -->

With everything cleared up, let's think about this algorithms time complexity. If the index is 0 it will be the fastest access possible. If it's the last element it will be the slowest possible. On average, as the list gets bigger so does our access, in a linear fashion that is. So O(n) it is.

#### Search

The algorithm for searching is almost identical to the one for accessing, the only difference is that we stop if we find the node with the value we are looking for.

```c
NODE* contributions;

int value_we_are_looking_for = 6;
NODE* pointer = contributions->next; //?
int counter = 0;

while(pointer != NULL){
    if(pointer->value == value_we_are_looking_for){
        return pointer;
    }
    counter++;
    p = p->next;
}
return NULL;
```

Much like accessing, we gotta go through every node and check their value independently. So exactly like accessing we would have a linear time complexity, cause the bigger the list size, the more nodes we gotta look for.

#### Insertion

Up until now you might be thinking, wow linked lists suck, compared to static arrays they are worse for accessing and the same for searching, why would anyone use them? Here is where they shine, inserting! At least for one specific type of insertion, pre-pending. If you want to insert a new node on the very beginning of our list, you have to do a simple pointer switcheroo. First we create the new node with the new value, then we take the pointer of this node and point it to the first node of the list. Lastly we take the initial pointer (the one pointing to the beginning of the list) and point him to our new node! Confusing? Check out this awesome animation.

# GIF for pointer switcheroo

Guess how much that costs us. The best time possible, constant time aka O(1). With the added benefit of our list never running out of space! Of course this would be different if we really wanted to add this node to the end of our list, at least the way we have the list setup now we do. On average this operation time would cost us O(n) time, just because we would have to go all the way to the position we want to insert. 

#### Deletion

Deletion has the same concept of inserting. We have to go to the node we wanna delete and then just switch the pointers around.

<!-- # GIF for pointer deletion switcheroo -->

An important note is that since we have to do all this memory management by ourselves in C, we can't forget to clear the space in memory the node was occupying previously.

### Common Linked Lists Questions

- Explain single linked lists like I'm five.
- What are some uses for linked lists?
- What are the differences between static arrays and linked lists?
- How adding and deleting works?
- What are the pros and cons?

### How it works on other languages

This datastructure has a lot of variations, too many to cover on this post, but what I can say is that when you do 

```python3
my_list = []
```
in python or elixir, what is happening behind the scenes is a linked list! That is very useful to know, you may think twice when adding elements to it. If you don't care about reversing the order you can pre-pend elements to make it super fast. 

If you are not careful you may do an algorithm with quadratic time complexity for not knowing this. Let me ilustrate it with an example:

```python3
all_numbers = [x for x in range(100)]

evens = []

for number in all_numbers:
    if(number % 2 == 0):
        evens.append(number) 
```

What is the time complexity for this algorithm? If you glance at it, you may think, it's linear, it only has 1 for loop, the bigger the all_numbers array is the longer the time linearly. But what you don't take into consideration is that evens.append is also linear time, but not from the same array. 

As we add elements to evens we need to go through every element of that list to get to the end and then add the new element. So our time would be O(n*k) where n is the size of all_numbers and k is the size of evens.

# Conclusion

Take a big breath cause this was quite a lot to take in! I don't expect for anyone to read through all of this in one sitting. This is something you gotta see a couple of times to sink it in.

What are some interview problems you have ran into? Comment down below!

Next up we'll talk about stacks, queues and doubly linked lists!
