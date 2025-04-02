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

## Avanços na Eficiência do Chaveamento de Contexto

Historicamente, a operação de troca de contexto representava um gargalo significativo nos sistemas operacionais, demandando consideráveis recursos computacionais. Esse processo exigia:

- Transferência completa do conteúdo dos registradores
- Armazenamento do estado do processador na memória principal
- Operações intensivas de I/O entre CPU e RAM

## Inovações em Arquitetura de Hardware

As modernas arquiteturas de processadores introduziram melhorias cruciais:

1. **Registradores Especializados**:
   - Conjuntos dedicados para armazenamento de contexto
   - Acesso rápido ao estado dos processos

2. **Hierarquia de Memória Avançada**:
   - Caches L1/L2 para estados de processo
   - Redução de acessos à memória principal
   - Buffers de transição otimizados

3. **Técnicas de Paralelismo**:
   - Hyper-Threading para execução simultânea
   - SMT (Simultaneous Multi-Threading)
   - Núcleos físicos virtuais

## Aprimoramentos em Algoritmos de Escalonamento

Os modernos sistemas implementam:

- **Heurísticas Inteligentes**:
  - Análise de padrões de execução
  - Previsão de necessidade de troca

- **Vinculação a Núcleos (CPU Affinity)**:
  - Associação estática de processos
  - Minimização de migração entre núcleos
  - Redução de invalidamento de cache

- **Balanceamento Dinâmico**:
  - Distribuição adaptativa de carga
  - Consideração de afinidade

## Impacto no Desempenho do Sistema

Estas otimizações proporcionaram:

- Redução de 60-80% no overhead de troca
- Melhoria de 30-50% no throughput do sistema
- Latência reduzida para aplicações críticas
- Eficiência energética aprimorada

## Aplicações em Ambientes Modernos

Particularmente benéfico para:

- Sistemas de tempo real
- Ambientes virtualizados
- Computação de alto desempenho (HPC)
- Nuvens computacionais
