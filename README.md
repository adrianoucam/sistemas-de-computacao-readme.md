# Laboratório Interativo de Sistemas Operacionais

**Simulador educacional de processos, memória, paginação, escalonamento, sincronização e deadlocks — executado diretamente no navegador.**

Este projeto reúne experiências visuais para apoiar aulas e atividades práticas de **Sistemas Operacionais** em cursos de graduação em Informática, Ciência da Computação e áreas afins. Os estudantes podem alterar parâmetros, avançar operações passo a passo, observar o estado do sistema e discutir as decisões tomadas pelos algoritmos.

> **Objetivo didático:** compreender o *porquê* das decisões de gerenciamento de recursos, e não apenas memorizar os resultados dos algoritmos.

## 🚀 Como executar

**Não é necessário instalar Python, Node.js, servidor web ou bibliotecas.**

1. Baixe o repositório usando **Code → Download ZIP** e descompacte-o; ou clone-o:
   ```bash
   git clone [https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git](https://github.com/adrianoucam/sistemas-de-computacao-readme.md.git)
   ```
2. Abra o arquivo **`index.html`** em um navegador atualizado (Chrome, Firefox ou Edge).
3. Escolha uma das abas do laboratório, configure o experimento e use os controles para simular.

O programa utiliza **HTML, CSS e JavaScript puro** e foi planejado para funcionar localmente, **sem conexão com a internet**. Se estiver utilizando uma versão do repositório que guarda o HTML na pasta `simulador_memoria/`, abra `simulador_memoria/index.html`.

## 📚 Conteúdos disponíveis

| Módulo | Conteúdo | Experimentos principais |
|---|---|---|
| **1. Alocação contígua** | Alocação e fragmentação externa | First Fit, Best Fit, Worst Fit, liberação e compactação |
| **2. Estados e bloqueios** | Ciclo de vida de processos e sincronização | Pronto, executando e bloqueado; E/S; `lock()`, `unlock()`, espera circular e deadlock |
| **3. Paginação e memória virtual** | MMU, tabela de páginas e TLB | VPN, PFN, offset, tradução de endereços, page fault e quadros físicos |
| **4. Substituição de páginas** | Políticas de substituição | FIFO, LRU, Segunda Chance, Relógio, Ótimo e anomalia de Belady |
| **5. Exercícios guiados** | Problemas sobre memória virtual | Endereçamento de 32 bits, tabela de páginas, EAT e page faults |
| **6. Aula 15 — Gerência da RAM** | Estratégias de gerenciamento da memória principal | Registradores base/limite, swapping, listas encadeadas, mapa de bits, Next Fit, Quick Fit e fragmentação |
| **7. Algoritmo do Banqueiro** | Evitação de deadlock | Matrizes Allocation, Max e Need; Available; Work/Finish; sequência segura e requisições |
| **8. Laboratório integrado** | CPU, memória, E/S e mutexes | Relógio lógico, estados/PCB, Gantt, quadros de RAM, grafo de recursos, detecção e recuperação de deadlock |
| **9. Lista 2.2 — Resoluções animadas** | Escalonamento, concorrência e impasses | Resolução guiada de cinco exercícios, com evolução passo a passo |

### 🧠 Alguns conceitos essenciais

- **Processo bloqueado ≠ deadlock:** um processo pode aguardar E/S ou um recurso e depois prosseguir; no deadlock, um conjunto de processos não consegue progredir devido à dependência circular de recursos.
- **Fragmentação interna ≠ externa:** a interna é espaço desperdiçado dentro de uma unidade alocada; a externa corresponde à dispersão de espaços livres.
- **Endereço virtual ≠ físico:** a MMU traduz o número da página virtual (VPN) no quadro físico (PFN), mantendo o deslocamento (*offset*).
- **Estado seguro ≠ estado sem processos bloqueados:** o Algoritmo do Banqueiro procura uma sequência em que todos possam terminar. Um estado inseguro **não implica necessariamente** um deadlock já existente.

## 🧪 Roteiro de atividades para os alunos

### Atividade A — Memória contígua

1. Abra **Alocação contígua** e escolha *First Fit*.
2. Aloque processos de tamanhos diferentes, depois libere um processo intermediário.
3. Observe os espaços livres e tente inserir um processo maior do que cada lacuna isolada.
4. Repita usando *Best Fit* e *Worst Fit*; compare a localização escolhida e os espaços restantes.
5. Experimente **Compactar** e explique por que essa operação pode ser custosa.

**Questão:** por que pode falhar uma alocação mesmo quando a memória livre total é suficiente?

### Atividade B — Tradução e falta de página

1. Abra **Paginação e memória virtual**.
2. Acesse o endereço virtual `0x21A4` e identifique **VPN** e **offset**.
3. Observe se ocorre page fault e acompanhe o quadro físico escolhido.
4. Repita um acesso à mesma página para verificar a influência da TLB.
5. Acesse páginas adicionais até provocar substituição na RAM.

**Questão:** o que se mantém constante durante a tradução de endereço e por quê?

### Atividade C — Substituição de páginas

Use **4 quadros inicialmente vazios** e a sequência:

```text
0, 1, 7, 2, 3, 2, 7, 1, 0, 3
```

Execute com **FIFO**, **LRU** e **Segunda Chance**. Registre o conteúdo dos quadros e o número total de faltas de página. Depois, use o exemplo de **anomalia de Belady** para discutir por que mais quadros podem causar mais faltas com FIFO em determinadas sequências.

### Atividade D — Lock, unlock e deadlock

1. Abra **Estados e bloqueios** ou **Laboratório integrado**.
2. Execute o cenário de concorrência normal, acompanhando aquisições e liberações de mutexes.
3. Execute o cenário de **deadlock**: P1 retém R1 e espera R2; P2 retém R2 e espera R1.
4. Observe o ciclo no **grafo de alocação de recursos (RAG)**.
5. Aplique a recuperação do cenário e compare com a **aquisição ordenada** (R1 antes de R2).

**Questão:** qual condição necessária para deadlock a ordenação global dos recursos procura eliminar?

### Atividade E — Algoritmo do Banqueiro

A configuração padrão contém **5 processos** (P0–P4) e três tipos de recursos, com totais **A = 10**, **B = 5** e **C = 7**.

1. Verifique a matriz **Allocation** e a matriz **Max**.
2. Calcule manualmente **Need = Max − Allocation** e compare com o programa.
3. Confira o vetor inicial **Available = [3, 3, 2]**.
4. Execute o **algoritmo de segurança** passo a passo, acompanhando **Work** e **Finish**.
5. Encontre uma **sequência segura**.
6. Teste uma solicitação, por exemplo **P1 → [1, 0, 2]**, e analise se a concessão preserva a segurança do sistema.

**Questão:** por que uma solicitação dentro de Available ainda pode ser adiada?

## 📝 Lista 2.2 — Exercícios com resolução guiada

A aba **9. Lista 2.2 — Resoluções animadas** organiza os cinco problemas da lista de **Escalonamento de Processos, Concorrência e Tratamento de Impasses**:

| Exercício | Assunto | O que observar |
|---|---|---|
| **1** | FCFS, SRTN e Round Robin (quantum de 3 ms) | Diagrama de Gantt, sobrecarga de 1 ms nas trocas de contexto, retorno, espera e eficiência da CPU |
| **2** | MLFQ (filas com quantum de 4 e 8 ms e fila FCFS) | Rebaixamento de prioridade, starvation e aging |
| **3** | Transferências bancárias com POSIX Threads | Intercalação de mutexes, deadlock, ordenação global e `trylock()` com backoff |
| **4** | Grafo de alocação com 5 processos e 5 recursos | Ciclo de deadlock, bloqueio direto versus indireto e recuperação por aborto de processo |
| **5** | Algoritmo do Banqueiro | Matriz de necessidades, vetor disponível, sequência segura e análise de uma requisição |

**Sugestão de uso em aula:** peça que os estudantes resolvam uma etapa *antes* de clicar em **Próxima etapa**. Compare as previsões da turma com o rastreamento exibido pelo programa.

> **Atenção:** convenções de escalonamento (por exemplo, ordem de eventos simultâneos e cobrança de troca de contexto) interferem nos resultados. Ao responder uma questão, siga explicitamente as regras do enunciado e do cenário selecionado.

## 🗂️ Organização do repositório

Estrutura mínima sugerida:

```text
laboratorio-sistemas-operacionais/
├── index.html          # Simulador completo
└── README.md           # Este guia
```

O simulador é autocontido em `index.html`. Não é necessário publicar os arquivos auxiliares de testes utilizados durante o desenvolvimento.

## 🛠️ Tecnologias

- **HTML5** — estrutura da interface;
- **CSS3** — organização visual, estados e animações;
- **JavaScript** — lógica dos algoritmos e atualização das simulações;
- **CSV** — exportação de eventos em partes do laboratório integrado.

## ♿ Acessibilidade e uso em laboratório

Recomenda-se projetar a aplicação em tela grande e utilizar o avanço **passo a passo** durante a explicação. As cores ajudam a diferenciar os estados, mas o aluno deve também ler os rótulos e registros de eventos. Para atividades avaliativas, registre os parâmetros do cenário, a sequência utilizada e as regras adotadas pelo algoritmo.

## ⚠️ Limitações do simulador

Este projeto é uma **representação didática simplificada**. Não executa um kernel real, não modifica a memória física do computador, não implementa sincronização entre threads nativas e não reproduz todos os detalhes de Linux, Windows ou outros sistemas operacionais. Alguns tempos, tamanhos, custos e políticas são fixados para facilitar a compreensão. Os resultados devem ser interpretados de acordo com cada cenário e suas hipóteses.

## 🤝 Como contribuir

São bem-vindos relatos de erros, propostas de exercícios, melhorias de acessibilidade e novas visualizações.

1. Abra uma **Issue** descrevendo o problema ou a ideia.
2. Informe a **aba**, os **parâmetros** do experimento, o **resultado observado** e o **resultado esperado**.
3. Se desejar contribuir com código, crie um **fork**, faça as alterações e envie um **Pull Request**.

Para exercícios novos, inclua preferencialmente: **enunciado, parâmetros, resolução comentada, etapas visuais e resultado esperado**.

## 📖 Referências e material de apoio

O conteúdo foi organizado a partir das apresentações e da lista de exercícios fornecidas para a disciplina **MC33 — Sistemas de Computação**, do **IMPA Tech**, ministrada pelo **Prof. Marcelo Maia**:

- **Aula 15:** Estratégias de gerenciamento da memória principal;
- **Aula 16:** Memória virtual e paginação;
- **Aula 17:** Algoritmos de substituição de páginas;
- **Lista de Exercícios 2.2 (2026/2):** Escalonamento de Processos, Concorrência e Tratamento de Impasses (Deadlocks).

Projetos públicos usados como referências de ideias de visualização e interação (sem implicar reutilização de código):

- [OS Teaching Tools](https://github.com/nasimbayati/os-teaching-tools)
- [OS-PhiloSim](https://github.com/meisamith/os-philosim)
- [OS Simulator](https://github.com/mazk36/os-simulator)

## 📄 Licença

**Licença ainda não definida.** Antes de publicar como projeto de código aberto, o responsável pelo repositório deve escolher uma licença e adicionar o arquivo `LICENSE`. Não presuma que a publicação no GitHub, por si só, conceda permissão de reutilização. Os materiais originais da disciplina devem ser compartilhados apenas com a autorização apropriada.

---

**Aprenda experimentando:** configure um cenário, antecipe a próxima decisão do sistema operacional, avance um passo e explique o resultado.
