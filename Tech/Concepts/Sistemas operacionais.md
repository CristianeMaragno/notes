
- Monotarefa: Executa apenas um programa por vez.
- Multitarefa: Executa diferentes programas quando é necessário esperar operações de entrada/saída.
- Tempo Compartilhado: O scheduler (escalonador) alterna rapidamente entre múltiplos programas.

**Conceitos**

- Processos: Instância de um programa. A execução de um programa na memória.
- Espaço de Endereçamento: Torna possível "existir" mais memória principal (RAM) do que existe fisicamente, pois cada programa utiliza endereços virtuais que são mapeados para endereços físicos.

**Estrutura**

- Em SOs unix-like, é comum usar a estrutura monolítica, quando o SO inteiro é executado como um único programa.
    - Os usuários interagem com o shell, compiladores e interpretadores.
    - Uma interface recebe as chamadas de sistema e traduz para o Kernel.
    - O Kernel faz a administração de sinais I/O, gerencia arquivos e faz o scheduling da CPU.
    - Por meio de uma outra interface, o Kernel se comunica com o hardware que realiza a execução das operações.


**Chamadas do sistema (syscalls)**

- Quando um processo que está sendo executado chama uma função do SO:
    - O sistema operacional é executado em alguns modos:
    - Kernel: Qualquer operação pode ser executada e qualquer memória acessada. Quando uma chamada de sistema ocorre, o sistema entra nesse modo.
    - Usuário: Permissões reduzidas.

**Interrupções**

- Quando um dispositivo I/O que está sendo utilizado, ele sinaliza para o processador (Interrupção), assim o processador executa uma rotina para lidar com essas interrupções. Em todo o resto do tempo o processador fica ocupado com a execução de outros programas.
    - Interrupções também podem ocorrer por conta de erros ou por conta de instruções de software (TRAP).

**Ciclo de vida de processos**

- New: Processo acabou de ser criado, por exemplo, por um fork.
- Running: Processo sendo executado na CPU, um por core.
- Ready: Processo carregado na memória principal e está aguardando para ser executado.
- Suspend Ready: Normalmente há muitos processos prontos, então alguns ficam no disco.
- Blocked: Processo não pode ser executado até finalizar I/O operação.
- Suspend Blocked: Similar ao ready.
- Destroyed: Processo que completou a execução.

**Hierarquia de processos**

- Quando o SO inicia (boot), um processo privilegiado é criado (processo init no Linux).
- Esse processo inicial cria outros processos filhos e esses, por sua vez, criam seus filhos... Assim é criada a árvore de processos.
    - O processo pai pode executar junto com os filhos ou esperar que um ou todos terminem.
    - O filho pode ser um duplicado do pai (usando fork()) – o pai e o filho seguem a execução após o comando ser chamado.
    - O processo pode chamar um outro programa (usando exec() ou similar).

**Threads**

- São tarefas de um processo executadas concorrentemente. Todo processo possui uma thread ao ser criado, mas pode criar outras.
    - Todas as threads compartilham recursos do processo.
    - Cada thread tem seu contador de programa (qual instrução está executando), seus registradores, armazenar suas variáveis, pilha de execução, estado.
    - Mas compartilham o espaço de endereçamento, variáveis globais, arquivos abertos e sinais e informações do processo.
    - O POSIX é uma biblioteca que segue um padrão de interface aceito para a manipulação de threads.

**Race condition:** Quando duas Threads tentam acessar o mesmo recurso do computador, erros podem ocorrer. A condição de corrida é um cenário onde a saída/resultado pode ser diferente dependendo da ordem de execução. Para evitar inconsistências, é necessário utilizar estratégias de sincronização:

- **Mutex:** A shared variable that can lock() or unlock() a region that a critical section is being executed. Deve ser usado com cuidado, pois limita a concorrência entre threads.
- **Semáforos:** É um tipo abstrato de dados que contém um contador interno e uma fila de tarefas que estão aguardando o semáforo. O contador pode ter valores negativos. Usa wait() e o post() para fazer o controle.

**Impasses (Deadlocks):** Mecanismos de controle de concorrência são necessários para evitar inconsistência de dados, porém, essa prática pode gerar impasses (deadlocks) – situação onde dois ou mais processos ficam esperando indefinidamente por um evento. Para que ocorra um deadlock, existem algumas condições que devem ser satisfeitas simultaneamente:

- **Exclusão mútua:** Apenas uma tarefa pode acessar o recurso por vez.
- **Segurar/espera:** A tarefa que detém o recurso espera por outro.
- **Recurso não preemptível:** Recurso não pode ser retirado de uma tarefa forçadamente.
- **Espera circular:** Entrave de espera de 2 ou mais tarefas por um recurso.

**Os métodos para evitar deadlocks são:**

- **Ignorar:** Pois se o sistema não é crítico e a possibilidade de deadlock é baixa, pode valer a pena ignorar.
- **Prevenção:** Eliminar uma ou mais condições que geram deadlock.
- **Anulação do deadlock:** Quando o escalonador percebe que a inicialização de um processo pode levar a um impasse, então o processo não é criado. Esse método exige que o escalonador tenha conhecimento profundo sobre os processos previamente.

**Outros conceitos relacionados:**

- **Inanição (Starvation):** A tarefa nunca ganha o processador por causa dos esquemas de sincronização.
- **Livelock:** Semelhante ao deadlock, exceto que é constante. Exemplo: Dois passos em um corredor que sempre escolhem o mesmo lado para desviar.

**Escalonamento de Tarefas:** Em sistemas multiprogramados, as tarefas competem pela CPU, por isso é necessário algoritmos de escalonamento eficientes, que visem alta utilização do processador, alta vazão (processos finalizados por unidade de tempo), baixo tempo de resposta e justiça na alocação da CPU. Alguns desses algoritmos são:

- **FCFS (First-Come, First-Served):** Processos são executados por ordem de chegada.
- **JF (Shortest Job First):** Processos com menor tempo são executados primeiro. É ótimo, só traz a dificuldade de identificar previamente qual o tempo de cada processo.
- **Round Robin:** Cada processo recebe uma pequena unidade de tempo (quantum).
- **Prioridade:** Um número de prioridade é associado a cada processo e a CPU é alocada ao processo com maior prioridade. Pode gerar inanição (Starvation).

**Exemplo de semáforos:** Semáforos são um método de sincronização muito útil pois evitam incrementos sucessivos e podem ser usados em muitos cenários. Os comandos principais são:

Wait(Sem)
SE Sem.contador > 0 ENTÃO
    Sem.contador = Sem.contador - 1
SE NÃO
    bloqueia a tarefa que faz a chamada
    insere a tarefa na fila

post(Sem)
SE fila não está vazia ENTÃO
    libera a tarefa no início da fila (sem.queue)
SE NÃO
    Sem.contador = Sem.contador + 1

**Exemplo de código – Leitores e escritores**

```
sem_t mutex, writeblock;
int data;
sem_init(&mutex, 0, 1);
sem_init(&writeblock, 0, 1);

void *reader(void *arg) {
    int f = *((int *) arg);
    sem_wait(&mutex);
    rcount = rcount + 1;
    if (rcount == 1)
        sem_wait(&writeblock);
    sem_post(&mutex);

    // Lê dados
    sem_wait(&mutex);
    rcount = rcount - 1;
    if (rcount == 0)
        sem_post(&writeblock);
    sem_post(&mutex);
}

void *writer(void *arg) {
    int f = *((int *) arg);
    sem_wait(&writeblock);
    data++;
    sem_post(&writeblock);
}
```

