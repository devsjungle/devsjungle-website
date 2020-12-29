Doubly linked lists

Stacks
Queues

<!-- Attention Grabbing Intro! -->


<!-- Subheaders! -->

## Stacks
Stacks are very simple in their nature, but they can be used to solve harder problems using them. That's why they are super common during interviews. They are quite literally a stack of data, much like a stack of anything (books, money, pancakes) if we can only handle one element at a time it's always the topmost element in the stack. Either we add another pancake to our stack or we remove the first one from it. That's the idea behind them. Another way to describe their behavior is by the acronym FILO, First In Last Out.

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

A stack structure used in C would look something like:

```c
typedef struct  node_{
 int value;
 struct node_ *next;
} NODE;

typedef struct stack_{
 NODE* top;
} STACK;

void stack_setup(STACK* s) {
 s->top = NULL;
}
```


```c
int stack_size(STACK s) {
    NODE* p1 = s.top;
    int size = 0;
    while(p1) {
        size++;
        p1 = p1->next;
    }
    return size;
}
```

```c
void push_to_stack(int new_value, STACK* s) {
 NODE* new_node = (NODE*) malloc(sizeof(NODE));

 new_node->value = new_value;
 new_node->next = s->top;
 s->top = new_node;
}
```

```c
int pop_from_stack(STACK* s) {
 NO* aux;
 int new_value;
 if(!s->top) return(-1);
 aux = s->top;
 new_value = aux->value;
 s->top = s->top->next;
 free(aux);
 return(new_value);
}
```


### Time Complexity
The traditional operations don't make much sense when talking about stacks. Since the usability is so straight forward and limited the operations time complexity are also simple to reason with. The main topic I will show you are the common uses and interview questions they may show up on.
 
#### Operations

- Access: In a stack it's not common for us to go to anywhere beyond the topmost item. But since it's uncommon for us to have a pure stack data structure as I showed above, you can access elements below the first one, but that time complexity will depend on the language you are using, not because of the way you are using it.
- Search: Again same idea from accessing, we don't really search for things inside a stack, we just look at the topmost element from the stack!
- Insertion: Putting an item in a stack is quick and easy, in the real world if the stack is too big (imagine a mountain of money) it may be hard to put another element on top of it, but in a computer it doesn't matter the size of our stack, the time it takes to add a new element is always the same, which means constant time or O(1)!
- Deletion: Removing an item costs the same as inserting it, no matter its size! Also constant time O(1). 

### Common uses:


### Common Stacks Interview Questions


## Queues
Queues are a huge topic, the concept of queues are used in complex systems with a lot of modern technologies such as RabbitMQ, AWS SQS and Kafka to some extent. They are also used in algorithms to achieve elegant solutions to complex problems. 

### How do they work?
Just like stacks, queues can also be brought to the real world, a queue at a supermarket or for buying tickets or waiting for your next online match. A common term used to describe queues is the acronym FIFO, First In First Out, which is the whole point of a queue. Something that you will see is that in order for them to be optimized you have to know where is the first element and where is the last one. That way we can add and remove with constant time!
 <!-- But only that is not enough, you have to know their neighbors as well! -->

<!-- ALL algorithms are here, need to organize and cleanup -->

```c
typedef struct node_ {
 int value;
 struct node_ *next;
} NODE;

typedef struct {
 NODE* start;
 NODE* end;
} QUEUE;

// Queue setup
void setup_queue(QUEUE* q) {
    q->start = NULL;
    q->end = NULL;
}
```

```c
// calculate size
int queue_size(QUEUE q) {
    NODE* p;
    int size = 0;
    p = q.start;
    while (p) {
        size++;
        p = p->next;
    }
    return size;
};
```

```c
// insert item at the end of the queue
void push_to_queue(int new_value, QUEUE* q) {
    NODE* new_node;
    new_node = (NODE*) malloc(sizeof(NODE));
    new_node->value = new_value;
    new_node->next = NULL;

    if(q->next){
        q->next->next = new_node; // queue is not empty
    } else {
        q->start = new_node; // first insertion of queue
    } 
        
    q->next = new_node; 
}
```

```c
// retirar a value da frente ou -1
int pop_queue(QUEUE* q)
{
    NODE* aux;
    int new_value;

    if(!q->start) return(-1);

    new_value = q->start->value;
    aux = q->start;
    q->start = q->start->next;
    free(aux);

    if(!q->start) q->next = NULL; // queue is empty

    return new_value;
}

```

### Time Complexity
Just like stacks queues don't follow other data structures time complexity, it's very limited but very precise in its functionality. 

#### Access
#### Search
#### Insertion
#### Deletion
 
### Common Queues Interview Questions
### How it works on other languages?

<!-- Doubly Linked Lists -->

```c
typedef struct estrutura {
 int chave;
 int info;
 struct estrutura *prox;
 struct estrutura *ant;
} NO;
typedef struct {
 NO* cabeca;
} LISTA;

// Inicialização (encadeamento duplo, circular e com nó cabeça)
void inicializarLista(LISTA* l) {
 l->cabeca = (NO*) malloc(sizeof(NO));
 l->cabeca->prox = l->cabeca;
 l->cabeca->ant = l->cabeca;
}

// Último elemento da lista (encadeamento duplo, circular e com nó cabeça)
NO* ultimoElemLista(LISTA l) {
 NO* p = l.cabeca->ant;
 if(p == l.cabeca) return(NULL);
 else return(p);
}

// Inserção ordenada sem duplicações
bool inserirElemListaOrd(int ch , LISTA* l) {
 NO* novo;
 NO* ant;
 novo = buscaSeqOrd(ch, *l, &ant);
 if(novo) return(false);
 novo = (NO*) malloc(sizeof(NO));
 novo->chave = ch;
 novo->prox = ant->prox;
 novo->ant = ant;
 novo->prox->ant = novo;
 ant->prox = novo;
 return(true);
}
```