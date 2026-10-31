# Lab 22 — Complexity Analysis

## 1. Heap Height
Explain why a complete binary heap containing `n` entries has height `O(log n)`.
A binary heap that has n entries has a height of O(log n) because binary heaps have to complete each level before moving to the next level. Therefore, a heap of a height h has at most 2^h nodes on the levels that are the fullest, meaning that the number of nodes grows exponentially with its height. By rearranging our equation n = 2^h, we get h = O(log n).

## 2. Priority Queue Operations
Analyze `insert`, `min`, and `removeMin`, explicitly relating bubbling to heap height.
Insertion will take O(log n) time complexity. This is because the new entry is added at the end of the vector, and then the upHeap function will compare the added node with its parent and swap positions if the conditions are met. Since the node can move one level per step, it will take O(h) and therefore O(log n) time. If the vector is resized, it will take O(n) sometimes, but overall, the insertion is still O(log n) in the expected case.
Since the minimum entry is at the root of the heap, heap_.front() will be able to return the minimum entry in constant time. Therefore, the min() function will be O(1) time complexity.
The removeMin() function is O(log n) time complexity. This is because the root is replaced by the last entry, and then downHeap will move nodes down until the heap properties are restored. Since the heap can travel to the height (lowest level), it will be O(log n) time.

## 3. Adaptable Operations
Explain why a handle containing the current array index permits `remove(entry)` and `replaceKey(entry,key)` in `O(log n)`, while scanning for an entry would not meet the specification.
The handle of every entry will point directly to the entry, and the index field of each entry will also store its current position (index) in the vector. When entries are swapped, the index are also updated. Because of this, remove(entry) and replaceKey(entry, key) can find the entry in O(1) time, and then use bubble to restore heap order in O(log n). If there were no handle, the time complexity would become O(n) since the heap would need to traverse through the vector to find the entry. This would make the operation O(n) rather than O(log n).

## 4. Bottom-Up Construction
Explain why repeated insertion is `O(n log n)` in the worst case, while bottom-up construction is `O(n)`. Give an argument based on subtree heights rather than only stating the result.
Repeated insertion is O(n log n) in the worst case because each of the n amount of entries could bubble up through a maximum of O(log n) levels. On the other hand, bottom-up construction puts all entries in the vector and will call downHeap on the internal nodes. It will start from the lowest level and move toward the root. Even though a node can move down multiple levels, many of the nodes are near leaves and don't have much space to travel. A maximum of n/2^h+1 nodes are h (height) above the leaves, and each of these nodes can move a maximum of h levels. Therefore, the total amount of operations can be represented by the summation from h>=0 of nh/2^h+1 which gives us O(n) time complexity for bottom-up construction.

## 5. Heap Sort
State and justify time complexity, auxiliary-space complexity, and whether your implementation is in place.
Heap Sort requires O(n log n) time. This is because building the heap takes O(n) time, and then removing the maximum all the way to the end of the vector will take O(log n) per entry. Combining the two gives us O(n log n) time complexity for heap sort. My implementation is in place since the original vector is sorted without making the second vector. However, the heapify function is recursive, meaning it uses O(log n) space in the worst case. By switching heapify to in iterative implementation, the space ccomplexity becomes O(1).

## 6. Design Reflection
Compare a heap-based priority queue with unsorted-list and sorted-list implementations when both insertion and minimum removal need to be efficient.
An unsorted list has O(1) at the end of the list. However, finding and removing the minimum would require O(n) since we must do a traversal through the whole list to find the minimum and then remove it. 
On the other hand, a sorted list has O(n) time complexity, since there must first be a search for the proper insertion index. However, the minimum can be accessed and removed in O(1) time because since the list is sorted, the minimum element will be the first element in the list. 
A heap data structure gives us a balance between the two. Insertion, along with the removal of the minimum, are both O(log n) operations, with the reading of the minimum being O(1). Therefore, a heap is a good choice when both operations of adding elements and removing the minimum need to be efficient.
