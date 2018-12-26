### Chapter 8- Stacks and Queues in python

### Stacks

- stacks: last in, first out
  - supporting two basic operations: push and pop
  - if implemented with linked list, then it is O(1) time for both of the operations above
  - if implemented with dynamic list then it is amortized O(1) time for both of the operations above
  - or you can have peek, which returns the value of the top item without actually popping it
- stack implementation makes reversing a sequence of values extremely easy

```python
def print_linked_list_in_reverse(head):
    nodes = []
    while head:
        nodes.append(head.data)
        head = head.next
    while nodes:
        print(nodes.pop())
```

- this above code is time O(n) and space O(n)

### Tips for stacks

- recognize whenever the LIFO property is available. Parsing typically requires a stack 
- when practicing, you can consider augmenting stack or queues so that they have additional features, such as maximum/ minimum/ size/ etc

### Stack libraries

- the built-in list type contains the following nice features:
  - s.append(e) : pushes element e to stack s
  - s[-1] retrieves but not remove the top of the stack. This feature is similar to peek
  - s.pop() removes the first element of the stack and returns the value of the data
  - len(s) == 0 tests whether stack is empty

### Question 8.1 

- question: design a stack that includes the max operation that returns the max value on the stack. (in addition to implementing the basic push and pop method)
- **Idea 1** iterate through the stack, which uses O(n) time and O(1) space
- **Idea 2** using another data structure, such as heap or BST along with a hash table, wthis would require O(log n) time and O(n) space, but the codes are going to be complex
- **Note** calculating max on push is easy but it is not so easy with pop, since you would have to trace back in history to figure out what is the new max
- **Idea 3** Use caching. In this case we are tradig time for space, and for each entry in the stack we cache the maximum corresponding value



```Python
class stack:
    #named tuple records both the element value and the corresponding max value to that 		#element
    
    #ElementWithCachedMax is a structure that exists within stack
    #push and pop and the operator[-1] for stack is already defined as it is
    ElementWithCachedMax = collections.namedtuple('ElementWithCachedMax',('element','max'))
    
    def __init__(self):
        #this is the array that holds the structure ElementWithCachedMax, which
        #in itself holds the value and max
        self._element_with_cached_max == []
        
    def empty(self):
        retur len(self._element_with_cached_max ) == 0
    
    def max(self):
        if self.empty():
            raise IndexError('max(): empty stack')
        return self._element_with_cached_max[-1].max
    
    def pop(self):
        if self.empty():
            raise IndexError('pop(): empty stack')
        return self._element_with_cached_max.pop().element
    
    def push(self,x):
        self._element_with_cached_max.append(
            self.ElementWithCachedMax(x, x if self.empty() else max(x,self.max()))
    
```



Reference for namedtuple

https://pymotw.com/2/collections/namedtuple.html



- **Idea 4** Improve the best case space
  - Observe that if an element e that is being pushed is smaller than the maximum element already on the stack, then e will never be maximum. In this case it is meaningless to record e in the max value aspect
  - solution is to record the number of occurrence ofeach max value
  - look at page **100** for a more detailed explanation of this method. You have a auxiliary stack that holds the number of occurences of that value. detailed implementation is below

```Python
class Stack:
    class MaxWithCount:
        def __init__(self,max,count):
            # the MaxWithCount class is the type of objects held in _cached_max_with_count 				# stack, its max field holds the value of the max element and the count is the 
            # number of occurences for the corresponding interval
            self.max, self.count = max, count
            
    def __init__(self):
        # making two stacks, one for the max and one to hold its elements
        # the stack _cached_max_with_count holds the elements of type MaxWithCount
        self._element = []
        self._cached_max_with_count = []
        
    def empty(self):
        return len(self._element) == 0
    
    def max(self):
        if self.empty():
            raise IndexError('max():empty stack')
        return self._cached_max_with_count[-1].max
    
    def pop(self):
        if self.empty():
            raise IndexError('pop():empty stack')
        pop_element = self._element.pop()
        current_max = self._cached_max_with_count[-1].max
        #if the pop element is the max, then things need to be changed
        #otherwise, if the pop element is not the max it doesnt matter when you remove it
        if pop_element == current_max:
            #one less occurence of the max
            self._cached_max_with_count[-1].count-=1
            #when it's zero then you pop it
            if self._cached_max_with_count[-1].count == 0:
                self._cached_max_with_count.pop()
        return pop_element
    
    def push(self,x):
        self._element.append(x)
        if len(self._cached_max_with_count) == 0:
            self._cached_max_with_count.append(self.MaxWithCount(x,1))
        else:
            current_max = self._cached_max_with_count[-1].max
            if x== current_max:
                self._cached_max_with_count[-1].max +=1
            elif x > current_max:
                self._cached_max_with_count.append(self.MaxWithCount(x,1))
    
```

