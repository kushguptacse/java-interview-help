# Interview-Help
It covers some hands-on notes on various topic and resources required to clear interview
## Java
1. Integer i=127;Integer j=127; both i==j and i.equals(j) will give true. but for value >127 '==' operator gives false. Reason-> Whenever you are creating Integer objects using auto boxing, compiler rewrites that statement with Integer.valueOf(int i) method. This method is implemented such that the frequently used values are cached. I.e. internally it maintains an array of Integer objects for range from -128 to 127.<br/>
### Collection hierarchy
1. Below are popular interface, classes related to Collection and are present in java.util package-><br/>
2. For collection hierarchy visit -> https://dzone.com/articles/java-collections<br/>
3. **Iterable** interface provide iterator and foreach method.<br/>
4. **Collection** interface extends Iterable. provides general method like, add, addAll, remove, size(), isEmpty(), contains <br/>
5. **Set** interface extends Collection. is used to store unique un-ordered elements. method wise it does not contain own method apart from method inherited from Collection.<br/>
6. **SortedSet** interface extends Set. it has comparator, subSet, headSet, tailSet methods. e.g. tailSet(fromElement) Returns a view of the portion of this set whose elements are >= fromElement.  The returned set is backed by this set, so changes in the returned set are reflected in this set, and vice-versa.<br/>
7. **NavigableSet** interface extends SortedSet.(java 1.6). it provides lower,floor,ceiling,higher methods. ceiling(E e): Returns the least element>=e. higher(E e): Returns the least element>e. floor(E e): Returns the greatest element <=e. <br/>
8. **TreeSet** class implements NavigableSet. and is used when we want to maintain sorted data without duplicate.<br/>
9. **HashSet** class implements Set. and is used when we want to maintain data without duplicate. and order doesnot matters.<br/>
10. **LinkedHashSet** class extends HashSet. In it data is ordered and does not contain duplicates. It maintains a doubly-linked list running through all of its entries for maintaing order.<br/>
11. **List** interface extends Collection. is used to store ordered data. it can contains duplicates. it provides get(index), set(index,element), remove(index) methods also.<br/>
12. **ArrayList** class implements List. it stores data in array. faster when retreival operations are more.it also implement RandomAccess interface.initial capacity is 10. and when its full, new array is created with double size and prev array data is copied.<br/>
13. **Vector** class implements List. is also a re-sizable array similar to an ArrayList. Use it only when you need thread-safety and synchronization.it also implement RandomAccess interface<br/>
14. **Stack** class extends Vector. provides FIFO. its method are synchronized. push, pop, poll<br/>
15. **Queue** interface extends Collection. provides LIFO. has offer,peek, poll methods.<br/>
16. **PriorityQueue** class implements Queue. It is based on priorityHeap data structure (both max heap and min heap possible via comparator which if provided during constructor)<br/>
16. **Deque** interface extends Queue. can add and remove elements at both ends. addFirst,addLast,offerFirst,offerLast,pollFirst,pollLast <br/>
17. **ArrayDeque** class implements Deque. it is an implementation of Deque using an array for storage. <br/>
18. **LinkedList** class implements List and Deque interface.it is an implementation of Deque using Nodes for storage.<br/>
19. **Map** interface is used to store key,value pair.Methods are put, get, remove(key). It doesnot extends any interface. and keys are un-ordered.<br/>
20. **SortedMap** interface extends Map.it has comparator, subMap, headMap, tailMap methods.<br/>
21. **NavigableMap** interface extends SortedMap.(java 1.6). it provides lowerKey,floorKey,ceilingKey,higherKey methods.<br/>
22. **TreeMap** class implements NavigableMap. it is used when we want keys to be sorted. <br/>
23. **HashMap** class implements Map. and is used when we want to maintain data pair without duplicate keys. and key order doesnot matters.initial size is 16. when total elements exceeds initial size x loadFactor(0.75). map resizes to double of original size<br/>
24. **LinkedHashMap** class extends HashMap. In it keys is ordered and does not contain duplicates. It maintains a doubly-linked list running through all of its entries for maintaing order.<br/>
25. **Hashtable** class implements Map.and is used when we want to maintain data pair without duplicate keys. and key order doesnot matters. here methods are synchronized. <br/>
26. **Fail Fast** If we iterate through collection say arraylist. and during iteration itself if we try to modify underlying collection, ConcurrentModificationException will occur. <br/>
27. **Fail Safe** If we iterate through collection like **java.util.concurrent.CopyOnWriteArrayList** or **java.util.concurrent.CopyOnWriteArraySet**. and during iteration itself if we try to modify underlying collection, no exception will occur. this is becuase it work on copy of elements. so changes will not reflect in the loop itself. changes can be seen only after loop finishes. See https://github.com/kushguptacse/Thread for example<br/>
28. **java.util.concurrent.ConcurrentHashMap** It is fail safe. and during iteration itself if we try to modify underlying collection, no exception will occur and modified data can also be seen with in the loop. it is not keeping copy to iterate but uses semantics to avoid fail fast.<br/>
It uses locking of bucket level instead of locking entire collection like hashTable.
29. **java.lang.Comparable** interface provide public int compareTo(T o) method. wrapper classes,String class provide there own comparable for default sorting.<br/>
30. **java.lang.Comparator** interface provide public int compare(T o1,T o2) method. when we want to provide custom sorting then in such case we use it apart from default provided by comparable<br/>