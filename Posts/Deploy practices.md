ENG

The true utility of any application is realized when it actively engages with users, giving it a meaningful purpose. Deployment, the pivotal process of making software accessible, plays a crucial role in transforming potential into actual utility. In this post, I will delve into various deployment practices for web applications in particular.

It is essential to recognize that there is no one-size-fits-all solution in the realm of application development. To maximize effectiveness, it is imperative to comprehend your unique scenario and make informed choices that align with your specific objectives. Make yourself some questions.
#### Questions
- How many users do you expect?
- What's your budget?
- Can i give constant support to the system?
- I want to do things in the most efficient and cheap way or i want a easy deploy?
- How do you  plan to monitor your systems and identify bottlenecks?

**The basics**

When you have your answers and your project up and running, it's time for you to execute you application on a web server, a  very reliable computer that is always active, and can be accessed for anyone.
But, what happens if you have many users trying to execute your service at the same time? To solve this problem, you need a Load balancer.

**Load balancing**

To use all the cpus of your computer(Without using Threads), you create multiple processes of you application in different ports. To the user, their access a load balancer like [[NGINX]], HAProxy, Ingress(In Kubernetes) or other that are connected to the port 80 of your server and redirect the traffic to your process using technics like round robin or another. Is in the load balancer that you install your certificates and similars, avoiding to add that complexity in the process itself.
For very large applications, you can have multiple load balancers and even in different regions.

![[simple deploy.png|500]]

Every system's got its limits, and one pivotal aspect is the ability to discern indicators of a sluggish connection. Recognizing these signs is imperative as it prompts the implementation of scaling strategies.

One way to undestand the capacity of your application is using this simple calculation: 
Throughput: How many requests a application can respond per second. Ex: If your service takes 100ms to respond a request and has 4 processes, they can respond to 40 requests. 

**Scalling**

Scaling, in simple terms, refers to adjusting the capacity of a system to handle increased demand. 
- Vertically: You give more resources to the same machine. 
	- _Pros:_ Simplicity, usually suitable for small to medium-sized applications.
	- Cons: Limited scalability, may reach hardware constraints.
- Horizontally: You add more machines
	- Pros: Improved scalability, cost-effective distribution of load.
	- Cons: Complexity increases, may require load balancing and synchronization

**Connection pool**

Managing database connections is essential, but unchecked usage can strain system resources, leading to memory and processing constraints. To mitigate this, implementing a connection pool is a good plan. By setting limits on connections for both your application and database processes, you prevent potential resource exhaustion. When a client request is made, it taps into the connection pool, which opens a connection with your application or database. Once used, the connection is returned to the pool, ready for another process to utilize, eliminating the need to open new connections each time. This practice is particularly useful for Threads to avoid unnecessary connection openings.

![[pool.png|500]]

If the pools aren't enough, you can also add a pgbouncer to intermediate the connection with the database, that will use 75% of your database, but can let thousands of requests hanging before trowing an error. This can slower your application, because you're adding a queue, but can be cheaper than creating more containers.

**Caching**

You can use caching when many of your requests return the same result, like the homepage view. You save the data and if is not expired(not too old) you return to the user instead of making a new request.
To accomplish this, databases like Memcache or Redis are utilized. While these options may not provide the comprehensive guarantees of databases like PostgreSQL, they boast superior speed and cost-effectiveness.

**Databases**
We saw the caching databases, but for our main database you can have different characteristics for writing and reading.
- Relational databases: Fast reading, but slow writing because they follow ACID guarantees 
- NoSql: Less guarantee

A common strategy when you run queries that take a long time to be executed, you can create a read only copy used for BI/reports etc, without slowing down the application for the users

![[database.png|400]]

**Other strategies**
When you have moments with great flux of people(Like Blackfriday) you can also use queue on the frontend giving queue number or send the front end a message of finishing and put the action in another queue, freeing the person from waiting. Exist services dedicated to dealing with queues like RabbitMq, Apache Kaftka, ActiveMQ and others.

If all of this is still not enough or during in periods of great user influx (such as Black Friday), using a frontend queue system can be effective. This involves assigning queue numbers to users or sending a finishing message to the frontend while transferring the process to a separate queue. This not only alleviates the waiting time for users but also enhances overall system efficiency. Dedicated queue services like RabbitMQ, Apache Kafka, ActiveMQ, among others, specialize in such scenarios. Integrating these queue systems ensures a smoother and more satisfying experience for your users.

**Monitoring**
For large-scale applications, is important to know when/which part is causing problems, this is where monitoring tools step in, playing a crucial role in providing insights into various aspects of your application's health and efficiency. You can use monitoring tools like New Relic RPM and Scout.

**Content Distribution Network**

A Content Distribution Network (CDN) is used for optimizing the delivery of static resources such as images, HTML pages, and videos. Rather than relying solely on your server, you upload these resources to the CDN, which assigns a unique path. When your application requests a resource, let's say an image, it queries the CDN first. If the CDN has the resource cached, it promptly delivers it, reducing the load on your servers. Only in cases where the resource isn't cached does the CDN reach out to your servers.

PT

A verdadeira utilidade de qualquer sistema se mostra quando há interação com os usuários, dando-lhe um propósito significativo. O deploy, processo que busca tornar o software acessível, desempenha um papel crucial na transformação do potencial em utilidade real. Nesta postagem, irei discutir sobre várias práticas de deploy e soluções para problemas comuns em aplicativos web em particular.

Primeiramente, é essencial reconhecer que não existe uma solução única para todos os cenários no domínio do desenvolvimento de aplicações. Para maximizar a eficácia, é fundamental compreender o seu cenário único e fazer escolhas informadas que se alinhem com os seus objetivos específicos. Se faça algumas perguntas.

**Questões**
- Quantos usuários eu espero que acessem a plataforma?
- Qual é o meu orçamento?
- Posso dar suporte constante ao sistema?
- Quero fazer as coisas da maneira mais eficiente e barata ou quero uma implantação fácil?
- Como você planeja monitorar seus sistemas e identificar gargalos?

**O básico**

Quando você tiver suas respostas e seu projeto funcionando, é hora de executar sua aplicação em um servidor web, que é um computador muito confiável, sempre ativo e que pode ser acessado por qualquer pessoa.
Você pode expor seu app assim como você faz localmente, mas, o que acontece se você tiver muitos usuários tentando executar seu serviço ao mesmo tempo? Para resolver este problema, você precisa de um balanceador de carga.

**Balanceamento de carga**

Para usar todas as CPUs do seu servidor (sem usar Threads), você cria vários processos da sua aplicação em portas diferentes. Para o usuário, ele acessa um balanceador de carga como [[NGINX]], HAProxy, Ingress (No Kubernetes) ou outro que esteja conectado à porta 80 do seu servidor e redireciona o tráfego para o seus processos usando técnicas como round robin ou outras. É no balanceador de carga que você instala seus certificados e similares, evitando adicionar essa complexidade no próprio processo.
Para aplicações muito grandes, você pode ter vários balanceadores de carga e até mesmo em regiões diferentes.

Cada sistema tem seus limites e um aspecto fundamental para uma boa experiência para seus usuário é a capacidade de você perceber indicadores de uma conexão lenta e você rapidamente ajustar seu sistema. Essa alteração para que seu sistema consiga lidar com mais carga/acessos é chamada de scalling.

Uma maneira de entender a capacidade da sua aplicação é usar este cálculo simples de Throughput: quantas solicitações um aplicativo pode responder por segundo. Ex: Se o seu serviço leva 100ms para responder uma solicitação e possui 4 processos, eles podem responder a 40 solicitações.

**Scalling**

Escalar, em termos simples, refere-se ao ajuste da capacidade de um sistema para lidar com o aumento da demanda.
- Verticalmente: você dá mais recursos para a mesma máquina.
- _Prós:_ Simplicidade, geralmente adequada para aplicações de pequeno e médio porte.
- Contras: Escalabilidade limitada, pode atingir restrições de hardware.
- Horizontalmente: você adiciona mais máquinas
- Prós: Escalabilidade aprimorada, distribuição de carga econômica.
- Contras: A complexidade aumenta, pode exigir balanceamento de carga e sincronização

**Conjunto de conexões**

Gerenciar conexões de banco de dados é essencial, mas o uso descontrolado pode sobrecarregar os recursos do sistema, levando a restrições de memória e processamento. Para mitigar isso, implementar um pool de conexões é um bom plano. Ao definir limites nas conexões para os processos de aplicativo e de banco de dados, você evita o possível esgotamento de recursos. Quando uma solicitação do cliente é feita, ele acessa o pool de conexões, que abre uma conexão com seu aplicativo ou banco de dados. Uma vez usada, a conexão é devolvida ao pool, pronta para ser utilizada por outro processo, eliminando a necessidade de abrir novas conexões a cada vez. Esta prática é particularmente útil para Threads para evitar aberturas de conexão desnecessárias.

Se os pools não forem suficientes, você também pode adicionar um pgbouncer para intermediar a conexão com o banco de dados, que usará 75% do seu banco de dados, mas pode deixar milhares de solicitações suspensas antes de detectar um erro. Isso pode tornar seu aplicativo mais lento, porque você está adicionando uma fila, mas pode ser mais barato do que criar mais instâncias.

**Cache**

Você pode usar o cache quando seus requests retornam sempre o mesmo resultado, como a visualização de uma página inicial, por exemplo. Você salva os dados e se não estiver expirado (não muito antigo) você os retorna ao usuário ao invés de fazer uma nova requisição e consulta.
Para isso, são utilizados bancos de dados como Memcache ou Redis. Embora essas opções possam não fornecer as garantias abrangentes de bancos de dados como o PostgreSQL, elas apresentam velocidade e economia superiores.

**Bancos de dados**
Vimos os bancos de dados para cache, mas para nosso banco de dados principal você pode ter características diferentes para escrita e leitura.
- Bancos de dados relacionais: leitura rápida, mas escrita lenta porque seguem garantias ACID
- NoSql: Menos garantias de integridade dos dados, mas mais velocidade na leitura e escrita

Uma estratégia comum quando você executa consultas que demoram muito para serem executadas, você pode criar uma cópia somente leitura usada para BI/relatórios etc., sem deixar o aplicativo lento para os usuários

![[database.png|400]]

**Outras estratégias**

 Quando você tem momentos com grande fluxo de usuários (como Blackfriday) você pode usar estratégias que dão a impressão de agilidade como filas no frontend dando um número/senha ou enviar uma mensagem de finalização e colocar a ação em outra fila, liberando a pessoa da espera. Existem serviços dedicados a lidar com filas como RabbitMq, Apache Kaftka, ActiveMQ e outros.

**Monitoramento**

Para aplicações de grande escala, é importante saber quando/qual parte do sistema está causando problemas, é aqui que entram as ferramentas de monitoramento, desempenhando um papel crucial no fornecimento de insights sobre vários aspectos da saúde e eficiência da sua aplicação. Você pode usar ferramentas de monitoramento como New Relic RPM e Scout.

**Rede de distribuição de conteúdo**

Uma Rede de Distribuição de Conteúdo (CDN) é usada para otimizar a entrega de recursos estáticos, como imagens, páginas HTML e vídeos. Em vez de depender apenas do seu servidor, você carrega esses recursos no CDN, que atribui um caminho exclusivo. Quando seu aplicativo solicita um recurso, digamos uma imagem, ele consulta primeiro o CDN. Se o CDN tiver o recurso armazenado em cache, ele o entregará prontamente, reduzindo a carga em seus servidores. Somente nos casos em que o recurso não está armazenado em cache é que o CDN chega aos seus servidores.