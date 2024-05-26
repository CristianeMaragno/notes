#### Questions
- How many users do you expect?
- What's your budget?
- How do you monitor your systems and identify bottlenecks?


**Load balancing**

![[simple deploy.png|500]]

To use all the cpus of your computer(Without using Threads), you create multiple processes of you application in different ports. To the user, their access a load balancer like [[NGINX]], HAProxy, Ingress(In Kubernetes) or other that are connected to the port 80 of your server and redirect the traffic to your process using technics like round robin or another. Is in the load balancer that you install your certificates and similars, avoiding to add that complexity in the process itself.

For very large applications, you can have multiple load balancers  and even in different regions.

Throughput: How many requests a application can respond per second. If 100ms to respond a request and has 4 processes, they can respond to 40 requests

**Scalling**
- Vertically: You give more resources to the same machine
- Horizontally: You add more machines

**Connection pool**
Each connection with the database needs to be registered and that uses memory and cpu, so without a limit of your application process or database process, eventually you will be without memory or processing.

So, a way to ease the problem, we establish a limit of connections to our process and then the client request goes to the pool of connection that open a connection with your application or database and after is used, is returned to pool and other process can also use without having to open a new connection. This is used for Threads to not open new connections.
Verify the connections of you plan.
![[pool.png|500]]

If the pools aren't enough, you can also add a pgbouncer to intermediate the connection with the database, that will use 75% of your database, but can let thousands of requests hanging before trowing an error. This can slower your application, because you're adding a queue, but can be cheaper than creating more containers.

**Caching**
You can use caching when many of your requests return the same result, like the homepage view. You save the data and if is not expired(not to old) you return to the user instead of making a request.
For this task, you should use databases like Memcache or Redis, that don't give all the grantees that a database like postgress give, but are faster and cheaper.  
Some some all the data when reinitialized(Ex Memcached), and other will also save in disk and not loose the data(Ex Redis)

**Databases**
We saw the caching databases, but for our main database you can have different characteristics for writing and reading.
- Relational databases: Fast reading, but slow writing because they follow ACID guarantee 
- NoSql: Less guarantee

Also, if you run queries that take a long time to be executed, you can create a read only copy used for BI/reports etc, without slowing down the application for the users

![[database.png|400]]

**Other strategies**
If all of this is still not enough, or you have moments with great flux of people(Like Blackfriday) you can also use queue no frontend giving queue number or send the front end a message of finishing and put the action in another queue, freeing the person from waiting. Exist services dedicated to dealing with queues like RabbitMq, Apache Kaftka, ActiveMQ and others.

**Monitoring**
For a big application, is important to know which part is really causing the problem, so you can use monitoring tools like New Relic RPM, Scout 

**Content Distribution Network**
You put your static resources like images, html pages, videos, etc and then you put the CDN path instead of your server. When your applications requests a image, as a example, they will as the CND and if they don't have the resource cached, they will only ask once your servers.

**Examples**
