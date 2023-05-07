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
1. **transaction isolation levels**-> <br>
1.1 **Read uncommitted**- handles nothing<br> 
1.2 **Read Committed**- handles **dirty read**(T1 has done some update and before commiting it T2 reads that updated record. later T1 rollback. hence T2 has read data which never existed),Sol-> The transaction holds a read or write lock on the current row till it is committed and thus prevents other transactions from reading, updating, or deleting it. <br> 
1.3 **Repeatable Read** - handles **non repeatable read**(T1 has read row with some data,T2 now has updated value of same row and commit it,Now T1 if execute read query again for same row it will get different data).sol-> The transaction holds lock on all rows matching query criteria. <br> 
1.4 Serializable- handles phantom read(T1 retrieves a set of rows acc to search criteria. Now, T2 generates some new rows that match the search criteria for transaction T1). sol-> table level lock is taken. <br>
https://www.geeksforgeeks.org/transaction-isolation-levels-dbms/ <br>
2. **ACID property. atomicity, consistency, isolation and durability.**<br> https://www.geeksforgeeks.org/acid-properties-in-dbms/ <br/>
3. **Optimistic and Pessimistic Lock**: https://vladmihalcea.com/optimistic-vs-pessimistic-locking/ <br/>
4. **CAP -> https://www.scylladb.com/glossary/cap-theorem/<br>
4.1 **consistency** - Consistency of CAP theorem means that regardless of the node they connect to, all clients see the same data always.i.e. replication must be instant<br>
4.2 **Availability** - even if one or more nodes are down, any client making a data request receives a valid response. <br>
4.3 **Partition Tolerance** - in spite of any number of breakdowns in communication between nodes in the system, the cluster will continue to work.<br>
No sql supports partition tolerance always.<br>
AP - Cassandra<br>
CP - MongoDB<br> if master down, then till it is elected back system will not be available for write operation.<br>

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
21. to identify which query is taking long time?

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


### Spring
1. https://idemia.udemy.com/course/spring-interview-questions-and-answers </br>
2. life cycle of bean. https://howtodoinjava.com/spring-core/spring-bean-life-cycle/ </br>
3. https://stackoverflow.com/questions/10604298/spring-component-versus-bean</br>
4. @SpringBootApplication: It is a combination of three annotations @EnableAutoConfiguration, @ComponentScan, and @Configuration.</br>
5. **transaction propagation level**-> https://www.baeldung.com/spring-transactional-propagation-isolation<br>
@Transactional annotation is applied on class level or can also be applied to method level.<br>
REQUIRED, SUPPORTS, MANDATORY, NEVER, NOT_SUPPORTED, REQUIRES_NEW, NESTED 

### Microservices
1. **Monolith vs SOA vs Microservices** -><br>
1.1 **Monolith**->application is deployed as a single process. it is written in single language and has single database.<br>
1.2 **Software As Service - SOA**-> create independent service of different features like authentication, payment, order mngt. but still all are part of single deployment and use single database. it is better than monolithic as here code can be re-used and better organized which make manitainence easier. <br>
1.3 **Microservices**-> here each service is autonomous and deployed independently. they have seperate database. can be sacalled independently and can be written in different language. disadv-> here since every service needed to call other service either via api or async queue. there is some latency which was not there earlier in monolithic.<br>
In case needed,then only watch -> https://www.youtube.com/watch?v=XjpxyGEUzBs
2. sample microservice architecture->  https://idemia.udemy.com/course/microservices-interview-questions-passsing-guarranteed/learn/lecture/28869880#overview.<br>
3.**Blast radius** -> it tells degree to which system will get affected if microservice failed or shutdown. to make microservice blast radius less and make it more resilient-> we can make independent database for each microservice, implement circuit breaker,can opt async communication <br>
4.**Circuit breaker pattern** -> Here we set threshold to say 3. and circuit breaker service will act as proxy and checks if target service is reachable. if not and retry exhausts then it will instead of passing req to target can directly return info to caller. circuit breaker has 3 state-> open,closed and half-open. on closed state call to target is made. on open state circuit breaker itself return response and dont call target and on half-open, half req will be sent to target and half handled by circuit breaker.<br>
5. **event vs command** -> Event is something that had already been happened. and command is something that we want to be done. Generally, an event can be the result of the completion of a command. command can have priority and hence order can changed. but on other hand event since already happended and hence order is fixed. example-> after payment has been done, payment done event has been fired. after recieving event, order service updates order and publish 'send invoice' command to message broker or might call api. command has single consumer and multiple senders. event has multiple consumer and single sender.<br>
6. **managing distributed transactions** -> 2 Phase commit and saga are ways to manage it. <br>
6.1 **2 Phase commit protocol**-> 2 phase commit, in distributed transactions, transaction manager(cordinator) gives instruction to different resource manager( 1 RM for 1 db). so suppose tranasction depends on 3 db's. in first phase which is called prepare, The first phase is named ‘prepare’ and the coordinator queries participants if they are ready to finish with the commit. The second phase is named ‘commit’ and coordinator commands participants to commit and made changes visible to the outer world. Coordinator commands to commit only if all participants voted for it. If some of the participant votes ‘abort’ then the whole transaction and all participants are rolled back. It means any change made to the participant during the transaction is aborted. <br>
6.1.1 It is designed in a way that if node is saying they are ready in phase 1, they will never crash in phase 2, else that crashed node will be ignored. and suppose later that crashed node came back then by using log written on its machine they will perform commit. <br>
6.1.2 If cordinator node failed then in such case others nodes wait for the coordinator to be up again. or else they need to decide by themselves about fate of transactions which is generally not possible.<br>
6.1.3 It is synchronous is nature and hence not sutiable for long running transactions.<br>
6.1.4 it is not possible to implement in no sql database. for relational also they all must support cordintator node to be able to implement it.<br>
6.2 **SAGA pattern**->It is aysnchronous as here each microservice handle there own transaction. SAGA can be command based or event based.<br>
https://www.youtube.com/watch?v=WnZ7IcaN_JA<br>
6.2.1 **choreography**->It is event based. Here suppose customer placed order. order service create order and order create event is added into event queue(can be kafka). since payment service subscribed to order create event. it will receive it and perform payment. if it succeed or fail the payment done/not done event is fired and pushed into event queue. order service event handler receive it and update order status from pending to successful.disadv -> it might be possible to get deadlock if design is not correctly made. i.e. if 1 microservice depend on 2nd and 2nd on event created by 1st<br>
Here failure event will be used by microservice to decide there action and in such case compensating query needs to be fired to undo changes.<br>
6.2.2 **orchestration**->It is command based. here single central orchestrator service manages the transaction flow. disadv -> here it is so much depedent on central service. and change done in any service will affect central service.<br>
If any of the microservices encounter a failure, the orchestrator is responsible for invoking the necessary compensating transactions<br>











