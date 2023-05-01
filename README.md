# Interview-Help
It covers some hands-on notes on various topic and resources required to clear interview
## Java
1. Integer i=127;Integer j=127; both i==j and i.equals(j) will give true. but for value >127 '==' operator gives false. Reason-> Whenever you are creating Integer objects using auto boxing, compiler rewrites that statement with Integer.valueOf(int i) method. This method is implemented such that the frequently used values are cached. I.e. internally it maintains an array of Integer objects for range from -128 to 127.<br/>
2. if 2 interfaces has same default method and class implement both of the interfaces, in such case compile time error will come.</br>
3. interface Predicate<T>{ boolean test(T t); } </br>
4. interface Consumer<T>{ void accept(T t};} </br>
5. interface Function<T,R>{ R apply(T t);} </br>
6. interface Supplier<T>{ T get(); } </br>
7. In java 9, private and static method are allowed in interface.</br>
8. In java 9, We can create immutable collection by using static 'of' method for Set,List and Map. like List.of(1,2,3). prior to java 9 we need to use Collections.unmodifiableList type method.</br>
9. Prior to java 9, try with resource require resource needed to be created in->  try (Scanner sc=new Scanner()){}. but from java 9, resource created outside the try bracket can also be used inside it) -> Scanner sc=new Scanner(); try(sc){}.</br>
10. with java 10, var is also introduced, by it we can create local variable with type var and it will store that value which is assigned to it first. and after that we cannot change data type of that variable to some other value.</br>
11. in java 10, Collectors.toUnmodifiableList method is introduced, it will return UnmodifiableList directly from lambda. prior to java 10, from lambda expression, Collectors.toList method was there. by which we can add new data also later.</br>
12. In java 11, Optional class will now have isEmpty method. earlier it has only isPresent method. and we have to use ! operator with it.</br>
13. In java 11, String class will have isBlank method which will return true if string only has spaces. "hi\nhello\nhow\nare\nyou".lines().collect(Collectors.toList()), here it will split string using \n as delimeter and return list. str.strip() method will be just like trim, except it also removes unicode spaces like ('\u2000'+"hello").strip().</br>

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
27. **Fail Safe** If we iterate through collection like **java.util.concurrent.CopyOnWriteArrayList** or **java.util.concurrent.CopyOnWriteArraySet**. and during iteration itself if we try to modify underlying collection, no exception will occur. this is becuase it work on copy of elements. so changes will not reflect in the loop itself. changes can be seen only after loop finishes. <br/>
28. **java.util.concurrent.ConcurrentHashMap** It is fail safe. and during iteration itself if we try to modify underlying collection, no exception will occur and modified data can also be seen with in the loop. it is not keeping copy to iterate but uses semantics to avoid fail fast.<br/>
It uses locking of bucket level instead of locking entire collection like hashTable.
29. **java.lang.Comparable** interface provide public int compareTo(T o) method. wrapper classes,String class provide there own comparable for default sorting.<br/>
30. **java.lang.Comparator** interface provide public int compare(T o1,T o2) method. when we want to provide custom sorting then in such case we use it apart from default provided by comparable<br/>
### Thread
1. If we call run method on thread object. it will not be executed in a seprate thread. instead it will be invoked like normal method.</br>
2. If we call start method twice on thread. it will give IllegalThreadStateException exception when tried to call second time. <br/>
3. **Thread Life cycle** -> https://www.baeldung.com/java-thread-lifecycle <br/>
4. Callable, Deadlock, failfast and failsafe, OddEvenThread, ProduceConsumer. See https://github.com/kushguptacse/Thread for examples. <br/>
5. Lock can be either at instance level or at class level(by static method). and also instead of synchronizing entire method we can lock some part of it by using synchronized keyword. <br/>
6. Threads communicate with each other with the help of **wait and notify** method present on object class. wait and notify must be called inside synchronized block else IllegalMonitorStateException will be throwned. when wait is called, current thread release its lock and goes into waiting state. when 2nd thread which is now holding lock of same object call notify method. then other waiting thread will get chance to resume. NOTE - it is not mandatory that after calling notify method lock on object will be released instantly. in such case 1st thread might need to wait for lock to be available to resume. <br/>
7. wait, notify and notifyAll ar present in object class. as we take lock on objects not on threads.<br/>
8. t1.join() will make currently executing thread to wait for t1 to finish. it throws InterruptedException, when suppose currently running thread which is waiting for t1 to finish itself got interrupted. <br/>
9. **Shutdown hook** is a thread that implicitly invoked before jvm shutdown. addShutdownHook method takes thread as arg and is available in Runtime class.<br/>
10. **Deamon Thread** are low priority thread that runs on background. we can also make our own thread as deamon thread by calling setDaemon method on thread object else by default it will be user thread. garbage collector thread is example of deamon thread. When all user threads have completed their execution, the JVM terminate. at that time If JVM finds a running daemon thread, it terminates the thread and, after that, shutdown it. <br/>
11. **Thread.sleep** is static method. It pauses current thread but does not release lock.throws InterruptedException <br/>
12. **Thread.yield** is static method. it provides info to scheduler that current thread is ready to suspend the execution of the current thread. but it will depend on scheduler if it is suspended or not. just like sleep it also does not release lock. <br/>
### Database
1. transaction isolation levels -> https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/ <br/>
2. ACID property. atomic, consistent,integrety and durability. https://www.geeksforgeeks.org/acid-properties-in-dbms/ <br/>
3. 2 phase commit, in distributed transactions, transaction manager gives instruction to different resource manager( 1 RM for 1 db). so suppose tranasction depeends on 3 db's. first transaction manager gets the status of all 3 db's if transaction succeeds. after that TM sends instruction to each of the RM to commit. then only respective records are commited in the individual database, else rollback happen.<br/>
4. Optimistic and Pessimistic Lock: https://vladmihalcea.com/optimistic-vs-pessimistic-locking/ <br/>
### Security
1. CORS - cross origin request sharing. when 1 app from 1 domain want to access api from other domain. it will not be allowed by default. need to use @CrossOrigin anotation provided by spring. <br/>
2. CSRF - cross site request forgery. here in a browser window suppose linkedin is open and if another site get access valid session and by using it try to get info of linkedin that will be called CSRF. spring prevent it by using csrf filet which attach csrftoken with each req. and hence fake req will not have this token to get illegal info. <br/>

### Design pattern
1. creational -> singleton, prototype, builder, factory method.</br>
2. Structural  -> Adaptor, proxy, Decorator <br/>
3. Behavioral -> Iterator, template, chain of responsibility. <br/>

### sql
1. **DDL - Data definition language**. it is used to create db schema or structure. create, alter, drop, rename, truncate.<br/>
2. **DML - Data Manipulation language**. it is used to manipulate data of the table. select,insert,delete,update.<br/>
3. **Constraints** - not null, unique, primary key, foreign key.<br/>
4. **Truncate vs delete->** Truncate clean up entire table and also free up table space. delete can be conditional and will require commit or rollback command. Truncate cannot be rollbacked, delete can be. truncate is DDL, delete is DML. on delete we can bind triggers, but Truncate cannot.</br>
truncate from sales.</br>
5. **Trigger** can be executed before or after the 'insert','update' or 'delete' operation.</br>
6. **3 types of index-> unique index, clustered index, non-clustered index.** clustered index is created by default for primary key for every table, and data is arranged acc to it on table itself. Unlike a clustered index, a non-clustered index is stored in a separate location from the data table. It is like a book index, which is located separately from the main contents of the book. Since non-clustered indexes are located in a separate location, there can be multiple non-clustered indexes per table. If you want to select only the index value that is used to create and index, non-clustered indexes are faster. For example, if you have created an index on the “name” column and you want to select only the name, non-clustered indexes will quickly return the name.</br>
7. **Types of join -> inner join, left outer join, right outer join, full outer join and self join.** self join is joining table with itself. inner join is like intersection. left outer join will have all rows of left table and corresponding records of right table will be set to null if it does not have match.</br>
8. like operator does not use index hence should be avoided. prefere > or = wherever possible.</br>
9. **Dual table** is a special 1 row and 1 column table present by default in oracle database. it is used to select pseudo columns like sysdate, user, rownum etc. pseudo columns are like table column, but it is not actually stored in the table.You can only perform select query from pseudo columns<br>
10. we can insert rows in dual table also-> insert into dual values ('anything')<br>
11. how to backup table ->  create table backupsales as select * from sales<br>
12. we cannot drop all columns from table.<br>
13. Both are same -> select count(1) from dummy; select count(*) from dummy;<br>
14. **'in' vs '='** 'in' operator can take multiple values inside it. but '=' operator can only take 1 value. 'in' operator can take 99 values.<br>
15. **EXIST and IN diff in subquery->** https://www.javatpoint.com/in-vs-exists <br>
16. **WHERE vs HAVING->** where clause is executed first and it filter out data before aggregation. having is applied on group by filter. i.e. after the aggregation takes place.<br>
17. Order along with precedence-><br>
17.1 **FROM & JOINs** determine & filter rows<br>
17.2 **WHERE** more filters on the rows<br>
17.3 **GROUP BY** combines those rows into groups (it is not mandatory to use group by column in select column). <br>
select avg(age) from customers group by country<br>
A GROUP BY clause requires that every column that the query returns is either a column contained in the GROUP BY statement or an aggregate function (such as the COUNT). <br>
17.4 **HAVING** filters groups<br>
17.5 **ORDER BY** arranges the remaining rows/groups<br>
18. we can only do rollback on un-committed commands. once commit is done it is saved permanently.<br>
19. we can delete data from 2 tables simulatenously by using delete query and join those 2 tables.<br>
20. **Delete duplicate records->** first using count, group by and having we can find duplicate rows. then use delete query along with in clause and max function to remove one of them. complete example https://www.sqlshack.com/different-ways-to-sql-delete-duplicate-rows-from-a-sql-table/<br>

### AWS
1. Regions -> aws services are spread across multiple locations and they are called regions.</br>
2. Zones -> each region is further divided into zones. where every region has atleast 2 zones. if 1 zone goes down, other can serve. each availability zone can have multiple data centers.</br>
3. Edge locations-> to make it near to end customer, betweeen zone and user there is an edge locations, so that user traffic does not need to travel too much to reach zone, instead edge locations full fill the request. </br>
4. EC2 stand for elastic compute cloud. they are virtual servers.</br>
5. AMI stand for amazon machine image. it will have softwares that we want to part of machine once it launched.</br>
6. EC2 spot instance. by default ec2 is on demand instance. A Spot Instance uses spare EC2 capacity that is available for less than the On-Demand price. Because Spot Instances enable you to request unused EC2 instances at steep discounts, you can lower your Amazon EC2 costs significantly. When you use Spot Instances, you must be prepared for interruptions. Amazon EC2 can interrupt your Spot Instance when the demand for Spot Instances rises or when the supply of Spot Instances decreases. When Amazon EC2 interrupts a Spot Instance, it provides a Spot Instance interruption notice, which gives the instance a two-minute warning before Amazon EC2 interrupts it.</br>
7. Public vs elastic ip -> when we launch the ec2 instance it is assigned private and public ip address. public ip address is used by client to access the application on that machine. but whenever we restart the machine that address will get changed. for that elastic ip can be created which will remain same but we need to pay for that ip.</br>
8. If you stop the instance, we will not be charged. and we can start it back again later. but if terminate the instance it cannot be retrieved.</br>
9. To secure ec2 instance we can create inbound and outbound rules under security group. inbound rule define who can access into VM. and outbound define what can be accessed by vm.</br>
10. To do auto-scaling. first create launch config which include AMI and other config required to make ec2 instance ready to serve. second step is to create auto scaling group. where we specify scaling policy on basis of which scale up and down of ec2 instacnes should happen. like cpu,disk perct.</br>
11. We can create dev user with access to ec2 and s3 only. for that create new user via IAM. and assign desired policy to that user from set permissions section.</br>
12. SNS - simple notification service. it helps to react to events happening in other aws services. sender can send message to sns topic and all subscriber can recieve it if they register for it. sender can be our own microservices or aws own service like cloud watch alarm</br>
13. cloud watch service can monitor cpu usage and send the message to topic if it passes some threshold. then via subscriptions this message will be sent to desired target.</br>
14. S3 vs EBS vs EFS -> Simple Storage system i.e. s3 is an object store, it is used to store static data like images, log files etc.  EBS (elastic block storage) and EFS (elastic file storage) can be attached to EC2 for writing and reading data. key diff is that EBS can be mounted to 1 EC2 instance only, where as EFS can be mounted with multiple EC2 instances.</br>
15. s3 storage classes. in case needed go through -> https://www.geeksforgeeks.org/amazon-s3-storage-classes/ </br>
16. RDS and dynamo db of AWS- rds is relational database service. dynamo db is no sql db.</br>
17. Types of load balancers -> https://linuxhint.com/load-balancers-types-aws/ </br>











