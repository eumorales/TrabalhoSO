# Sistemas Operacionais

## Trabalho baseado no livro "Sistemas Operacionais" – Deitel

### 1- Chaveamento de Contexto (Context Switching)

A troca de contexto é um mecanismo essencial em sistemas operacionais multitarefa, permitindo que a CPU alterne entre diferentes processos em execução. Como um único núcleo de processador executa apenas uma tarefa por vez, o sistema operacional gerencia essa alternância de forma eficiente.

#### Etapas da Troca de Contexto:

1. **Salvamento do estado atual**: Os registradores, o contador de programa e outras informações de execução são armazenados para posterior retomada.
2. **Seleção do próximo processo**: O escalonador escolhe qual processo será executado em seguida.
3. **Restauração do novo contexto**: O estado do próximo processo é carregado nos registradores.
4. **Retomada da execução**: A CPU reinicia a execução do processo selecionado a partir do ponto onde ele havia parado.

#### Importância:
Esse mecanismo permite a concorrência e a otimização do uso da CPU, garantindo a execução eficiente de múltiplos processos, mesmo em sistemas com um único núcleo.

---

### 2- Interrupções e seu Tratamento

Interrupções são sinais que interrompem temporariamente a execução normal da CPU para que eventos prioritários sejam tratados, como operações de entrada e saída ou falhas no sistema.

#### Principais Tipos de Interrupções:

- **De hardware**: Geradas por dispositivos externos, como teclado e disco rígido.
- **De software**: Ocasionadas por chamadas de sistema ou instruções específicas.
- **De temporizador**: Emitidas pelo relógio do sistema para controle de tempo e escalonamento.
- **Exceções**: Ocasionadas por erros, como acesso indevido à memória.

#### Fluxo de Tratamento:

1. A CPU interrompe a execução atual e salva seu estado.
2. O sistema operacional identifica a origem da interrupção e aciona o tratador adequado.
3. Após a execução do tratador, o contexto original é restaurado e a execução do processo interrompido pode continuar.

---

### 3- Comunicação Interprocessos

Em diversos cenários, processos precisam trocar informações ou coordenar suas ações. Os principais métodos utilizados incluem:

- **Sinais**: Notificações assíncronas, como o sinal SIGKILL para finalizar um processo.
- **Troca de mensagens**: Comunicação direta entre processos por meio de envio e recebimento de mensagens, como em sockets.
- **Pipes**: Canais de comunicação unidirecionais utilizados para transmitir dados entre processos, exemplificados pelo operador `|` no terminal.
- **Memória compartilhada**: Permite que múltiplos processos acessem a mesma região de memória, proporcionando comunicação eficiente.

---

### 4- Processos em Sistemas UNIX/Linux

Nos sistemas baseados em UNIX, os processos são unidades fundamentais de execução, criadas e gerenciadas por chamadas de sistema.

#### Criação de Processos:

- `fork()`: Duplica um processo existente.
- `exec()`: Substitui o código de um processo por um novo programa.

#### Comandos para Gerenciamento:

- `ps aux`: Lista todos os processos ativos no sistema.
- `kill -9 PID`: Finaliza um processo de maneira forçada.
- `top`: Exibe informações em tempo real sobre o uso de recursos pelos processos.

#### Exemplo de Comunicação entre Processos:
```bash
cat arquivo.txt | grep "palavra"  
```

---

# Questão

Ao longo das décadas, o chaveamento de contexto passou por significativas otimizações para reduzir seu impacto no desempenho dos sistemas. Nas primeiras implementações, esse processo era extremamente custoso, exigindo a cópia completa de todos os registradores e estados do processador para a memória principal. Com os avanços na arquitetura de hardware, surgiram registradores dedicados para troca de contexto e mecanismos de cache especializados, que armazenam temporariamente os estados dos processos, minimizando os acessos à RAM e acelerando consideravelmente as operações de chaveamento.

Paralelamente, melhorias nos algoritmos de escalonamento contribuíram para reduzir trocas desnecessárias, como a implementação de heurísticas inteligentes de escalonamento e técnicas de CPU affinity, que mantêm processos relacionados executando no mesmo núcleo do processador. Tecnologias como Hyper-Threading e SMT (Simultaneous Multithreading) permitiram que um único núcleo físico gerencie múltiplas threads de forma mais eficiente, diminuindo a necessidade de chaveamentos completos de contexto. Esses avanços tornaram os sistemas operacionais modernos mais eficientes no gerenciamento de multitarefa, especialmente em ambientes que demandam alto desempenho e baixa latência.
