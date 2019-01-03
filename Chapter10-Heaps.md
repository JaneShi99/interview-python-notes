### Chapter 10-1 Heaps

### Heaps in Python

- heaps are specialized binary trees
- Heap invariant: the key at each node is at least as big as the keys stored at its children
- Heap has O(log n) fo rinsersion, O(1) time lookup for max element, and O(log n) deletion for max element.  O(n) for searching for a specific element
- The "extract max" operation is defined to delete and return the max element
- A heap can also be referred to as the priority queue.



### Heap usage example

- Heaps are good to use for "streaming fashion"
  - That is, suppose your task is to take continuous string inputs and your program computes the k longest strings in the sequence. (where the order does not matter)
  - A min heap can be useful. It supports efficient find min, remove min, and insert. 

```python
def top_k(k,stream):
    # Entries are compared by their lengths
    min_heap = [(len(s),s) for s in itertools.islice(stream,k)]
    heapq.heapify(min_heap)
    for next_string in stream:
        #push next string, then pop the shortest string in min_heap
        heapq.heappushpop(min_heap,(len(next_string),next_string))
    return [p[1] for p in heap.nsmallest(k,min_heap)]
```



- for the above code, each string is processed in O(log k) time. So altogether the time complexity of processing all of the data is log(n log k)
- it is possible to improve the best case time by comparing the new string's length first and only insert when the new length is greater than the length in the set

### Tips for using heaps

- Heaps are great when all you care about is the largest and smallest elements. Since you do not need to support fast lookup, delete, or search for arbitrary elements
- It is a good choice when you need to computer the k largest and the k smallest elements in a set. Use a min-heap, and max-heap respectively for each of these two scearios.

### The heap libraries

- heap functionality in python is provided by the "heapq" module.

```python
import heapq
heapq.heapify(L) #transform elements in L into a heap in-place, this is min heap
heapq._heapify_max(L) #transform elements in L into a max heap
heapq.nlargest(k,L) (heapq.nsmallest(k,L)) #returns the k largest(smallest) element in L
heapq.heappop(L) # pop from min heap
heapq._heappop_max(maxheap) # pop from a max heap
heapq.heappush(h,e) #pushes a new element e onto heap h
heapq.heappushpop(h,a) #pushes a on heap then pops and returns the smallest element
e = h[0] #peeking smallest element

```

