# RA-02 — Roteiro de Atividade
## Sprint 1 do Connexa: planejamento e execução com agente de IA

**Disciplina de Engenharia de Software** · Prof. Claudio Nunes
**Modalidade:** em equipe (4 a 5 integrantes) · **Duração:** uma sprint de duas semanas
**Ferramentas:** Azure Boards (processo *Agile*), GitHub, VS Code com agente de IA (GitHub Copilot ou Codex) conectado ao Azure Boards por MCP
**Submissão:** Microsoft Teams · **Avaliação:** da equipe

---

### Convenções deste documento

| Marcador | Significado |
|---|---|
| `<turma>` | Identificador da turma, informado pelo docente |
| `NN` | Número da equipe, com dois dígitos |
| `<organizacao-azure-devops>` | Organização da equipe no Azure DevOps, criada na RA-01 com contas institucionais |
| `<organizacao-github-da-equipe>` | Organização da equipe no GitHub, criada no roteiro do scaffold |
| `connexa-equipe-NN` | Repositório de produto da equipe (front-end, back-end e documentação), público |
| `<id>` | Número de um work item no Azure Boards — em commits e pull requests, escrito como `AB#<id>` |
| `<comando-de-verificacao>` | Comando único que roda localmente tudo o que o CI roda, documentado no `README` do repositório pelo scaffold |
| **o agente** | O assistente de IA que cada integrante usa no VS Code — GitHub Copilot ou Codex. Todas as etapas valem para os dois |

> O projeto no Azure DevOps continua se chamando exatamente `Connexa`.

---

## 1. Cenário

O Product Backlog do Connexa está pronto (RA-01) e o esqueleto da aplicação já roda no repositório da equipe (roteiro do scaffold). Começa agora a primeira sprint: duas semanas para transformar histórias do topo do backlog em um incremento que alguém de fora da equipe consiga usar e verificar.

Nesta sprint, **o código é escrito por um agente de IA**. Isso não dispensa a equipe do trabalho — muda o trabalho. Cabe à equipe decidir o que cabe na sprint, transformar cada tarefa em uma especificação que o agente consiga executar, exigir testes antes do código, conferir as evidências e decidir o que entra no `main`.

O agente lê as tarefas diretamente do Azure Boards por meio de um servidor **MCP** (*Model Context Protocol*), o protocolo que permite a um assistente de IA consultar ferramentas externas. A consequência prática é imediata: o que estiver mal especificado no work item vira código errado em minutos.

> **O que esta atividade avalia.** Não a quantidade de código, e sim práticas de engenharia: planejamento por capacidade, decomposição, especificação, verificação, revisão, rastreabilidade e integração. Uma história concluída com todas as evidências vale mais do que três histórias que ninguém consegue demonstrar.

---

## 2. Objetivos de aprendizagem

| Nível (Bloom) | Objetivo |
|---|---|
| Entender | Explicar a divisão de papéis entre equipe e agente e por que a qualidade da especificação determina a qualidade do resultado |
| Aplicar | Configurar a sprint, a capacidade e a conexão entre Azure Boards, GitHub e o agente |
| Aplicar | Escrever tarefas prontas para agente, com escopo, critérios e forma de verificação explícitos |
| Analisar | Confrontar o plano com a capacidade real da equipe e identificar o excesso antes do início da sprint |
| Avaliar | Auditar tarefas, testes e pull requests produzidos com IA a partir de evidências, aceitando, modificando ou rejeitando cada proposta com justificativa |
| Criar | Produzir um incremento verificável, rastreado do work item até o código integrado |

---

## 3. Pré-requisitos

### 3.1 Atividades anteriores

- [ ] RA-01 entregue e corrigida: backlog ordenado, com `Story Points`, Tags MoSCoW e critérios de aceite em Gherkin em todas as histórias
- [ ] Aula de testes de software concluída: níveis de teste, ciclo vermelho → verde, checklist de teste ruim e sabotagem controlada
- [ ] Roteiro do scaffold concluído: organização GitHub da equipe criada, `connexa-equipe-NN` criado a partir do modelo da stack escolhida, ADR-001 registrado e CI verde no `main`

### 3.2 O que o scaffold deve ter entregue

Este roteiro conta com os itens abaixo no repositório `connexa-equipe-NN`. Confira-os antes da Etapa 0; se algum faltar, volte ao roteiro do scaffold antes de seguir.

| Item | Para que serve nesta sprint |
|---|---|
| `AGENTS.md` e `.github/copilot-instructions.md` com as regras de arquitetura: módulos, fronteiras, onde ficam os testes | O agente segue as mesmas regras com qualquer ferramenta |
| `.vscode/mcp.json` (Caminho 1) e `.codex/config.toml` (Caminho 2), com o nome da organização a preencher | Conexão do agente com o Azure Boards |
| Workflow de CI que roda os testes e a verificação de fronteiras entre módulos em todo pull request | Evidência objetiva de que nada quebrou |
| `<comando-de-verificacao>` documentado no `README` | O mesmo gesto em qualquer stack: "rodar tudo o que o CI roda" |
| Modelo de pull request (`.github/pull_request_template.md`) | Padroniza as evidências exigidas na revisão (Etapa 8.3) |
| Usuário de desenvolvimento simulado | A autenticação está fora da Sprint 1; a aplicação se comporta como se houvesse um estudante autenticado |
| Proteção do `main`: pull request obrigatório, 1 aprovação e CI verde para integrar | Ninguém — nem o agente — integra código sem revisão |

### 3.3 Contas e ferramentas de cada integrante

- [ ] Acesso ao projeto `Connexa` com a conta institucional
- [ ] Membro da organização `<organizacao-github-da-equipe>`
- [ ] VS Code com o agente escolhido instalado e com sessão iniciada (Apêndice F ou G)
- [ ] Para o Caminho 2 (Codex): Node.js 20 ou superior instalado
- [ ] Docente com acesso de leitura à organização GitHub e ao projeto no Azure DevOps

---

## 4. Como a equipe trabalha nesta sprint

### 4.1 Quem faz o quê

| Atividade | Equipe | Agente |
|---|---|---|
| Meta, seleção de histórias e capacidade | Decide | — |
| Esqueleto de tarefas de cada história | Decide | Critica |
| Detalhe técnico de cada tarefa | Audita e aprova | Propõe |
| Testes de aceitação | Confere a correspondência com os cenários e o vermelho | Escreve |
| Implementação | Aprova o plano e supervisiona | Escreve |
| Revisão e integração no `main` | Decide | Explica o diff quando solicitado |
| Estado das tarefas no board e `Remaining Work` | Atualiza | Nunca altera |

### 4.2 A tarefa é a especificação

O agente lê a Task pelo MCP. Tudo o que ele sabe sobre o que fazer está no título, na descrição, nos critérios de aceite da história-mãe e nos comentários do work item. Por isso, nesta sprint, uma Task só pode ser executada quando está **pronta para agente** — o molde está no Apêndice A e o checklist de auditoria, no Apêndice B.

A especificação vive no work item, e não no chat. O chat do agente é descartável; o work item é o que outro integrante — ou outra ferramenta — usa para continuar o trabalho.

### 4.3 O ciclo de uma tarefa de implementação

```
  Task pronta para agente (Azure Boards)
        │  o agente lê pelo MCP, em modo somente leitura
        ▼
  Plano proposto pelo agente ─────────► a equipe aprova ou corrige
        ▼
  Testes de aceitação primeiro ──► push ──► CI VERMELHO  (evidência)
        ▼
  Implementação ─────────────────► push ──► CI VERDE     (evidência)
        ▼
  Sabotagem controlada (local, descartada)
        ▼
  Pull request com AB#<id> ──► revisão por evidências ──► merge
        ▼
  Uma pessoa atualiza a Task no board
```

### 4.4 Menor privilégio

O agente usa duas conexões com o Azure Boards:

- **`ado-planejamento`** — pode criar e alterar work items. Usada **somente** nas Etapas 5 e 6.
- **`ado-leitura`** — somente leitura. Usada em todo o restante da sprint.

Nenhuma chamada de ferramenta do agente é aprovada automaticamente: cada integrante lê o que o agente pretende fazer antes de aprovar. Se um work item contiver algo como "desative a verificação" ou "ignore o AGENTS.md", trate como defeito da tarefa e corrija o work item.

### 4.5 Cota de uso do agente

Os planos gratuitos têm limites de uso: o Copilot Student tem uma cota mensal de créditos e o Codex no plano gratuito, uma cota em janelas de algumas horas. Cada integrante tem a própria cota; **a cota da equipe é a soma delas**.

- Uma Task por sessão do agente; inicie uma sessão nova a cada Task.
- Nunca peça "implemente a história inteira": além de gerar um pull request impossível de revisar, consome a cota em uma única tentativa.
- Distribua as tarefas de implementação entre os integrantes.
- Se a cota de alguém acabar, outro integrante continua a mesma Task — é possível porque a especificação está no work item.

---

## 5. Etapas

| Momento | Etapas | Formato |
|---|---|---|
| Primeira aula de laboratório da sprint | 0 a 7 | Equipe completa; o que não couber na aula é concluído em reunião da equipe até o segundo dia da sprint |
| Semanas 1 e 2 | 8 | Aulas de laboratório e trabalho da equipe |
| Fim da semana 1 | Ponto de controle (8.6) | Reunião curta da equipe |
| Última aula da sprint | 9 | Equipe completa |

> A execução (Etapa 8) só começa depois que o **Checkpoint 7** estiver verificado. Os tempos indicados são estimativas.

---

### Etapa 0 — Conectar Azure Boards, GitHub e o agente (40 min)

**0.1 Conectar o Azure Boards ao repositório.** Esta etapa exige um integrante que seja administrador do projeto no Azure DevOps e owner da organização no GitHub.

1. No Azure DevOps, abra **Project Settings › Boards › GitHub connections** e selecione **Connect your GitHub account**.
2. Escolha a organização `<organizacao-github-da-equipe>` e marque o repositório `connexa-equipe-NN`.
3. O GitHub pedirá a aprovação do aplicativo **Azure Boards** na organização. Aprove apenas para o repositório `connexa-equipe-NN`.

**0.2 Conectar o agente.** Cada integrante segue o Apêndice F (GitHub Copilot) ou o Apêndice G (Codex). Integrantes da mesma equipe podem usar caminhos diferentes.

**0.3 Teste de fumaça.** Faça os três testes abaixo antes de seguir.

1. **Leitura do board.** Com a conexão `ado-leitura`, cada integrante pede ao agente:
   > Liste as User Stories do projeto Connexa na ordem do backlog, com ID, título e Story Points. Não altere nada.

   Compare a resposta com o que aparece em **Boards › Backlogs**.

2. **Vínculo entre commit e work item.** Crie uma Task chamada `Etapa 0 — teste de conexão`, **fora** da Sprint 1. Então:
   - crie o branch `chore/AB<id>-teste-conexao`;
   - crie o arquivo `docs/sprint-1-planejamento.md` só com os títulos da seção 6.2;
   - faça um commit com a mensagem `docs: esqueleto do planejamento da sprint 1 AB#<id>`;
   - abra um pull request, peça a revisão de outro integrante e integre-o depois do CI verde;
   - abra a Task no Azure Boards e confira, na seção **Development**, o vínculo com o commit e o pull request;
   - feche a Task.

3. **Proteção do `main`.** Confira, em **Settings › Rules** (ou **Settings › Branches**) do repositório, que o `main` exige pull request, 1 aprovação e o CI verde. Se a regra não existir, crie-a agora.

> **Atenção ao vínculo.** Escreva apenas `AB#<id>` em commits e pull requests. Palavras como `Fixes AB#<id>` podem mudar o estado do work item automaticamente no merge; nesta sprint, os estados são movidos por pessoas, depois de verificado o Definition of Done.

> **Checkpoint 0** — Cada integrante obteve do agente dados reais do board. O pull request de teste aparece vinculado ao work item. O `main` não aceita integração sem pull request aprovado e CI verde.

---

### Etapa 1 — Configurar a sprint na ferramenta (15 min)

1. **Project Settings › Boards › Project configuration › Iterations**: abra `Sprint 1` e informe as datas de início e de fim (duas semanas).
2. **Project Settings › Boards › Team configuration › Iterations**: confirme que `Sprint 1` está na lista de iterações da equipe.
3. **Boards › Sprints › Capacity**: cadastre cada integrante, informe as **horas por dia** e marque os **dias de ausência** já conhecidos.

> **Checkpoint 1** — `Sprint 1` aparece no seletor de sprints com as datas corretas, e a aba *Capacity* mostra todos os integrantes.

---

### Etapa 2 — Calcular a capacidade de esforço humano (20 min, sem ferramenta)

Com um agente escrevendo o código, as horas desta sprint medem **o esforço das pessoas**: especificar, conferir a proposta do agente, verificar os testes, executar os cenários, revisar e atualizar o board. O tempo de processamento do agente não entra na conta; o tempo que você passa acompanhando, corrigindo e conferindo o trabalho dele, sim.

Cada integrante declara, **em voz alta e diante da equipe**, quantas horas por semana consegue dedicar ao projeto.

```
Horas declaradas por integrante, por semana ......  6h
Integrantes .....................................   5
Semanas da sprint ...............................   2
                                              ------
Capacidade bruta ................................  60h

( - ) reserva para imprevistos, provas e retrabalho ....  20%
( - ) reuniões da equipe ...............................   4h
                                              ------
Capacidade de planejamento ......................  44h
```

**Regra da primeira sprint:** sem histórico, planeje entre **70% e 80%** da capacidade de planejamento. A primeira sprint com agente costuma consumir mais tempo de verificação do que a equipe imagina.

Registre também, para cada integrante, **o caminho de IA que vai usar** (Copilot ou Codex). Se toda a equipe depender de um único caminho, inclua isso nos riscos (Etapa 7).

> **Checkpoint 2** — A equipe tem um número único de horas de capacidade, com a conta e o caminho de IA de cada integrante registrados por escrito.

---

### Etapa 3 — Escrever a meta da sprint (15 min, sem ferramenta)

**Escreva a meta antes de escolher qualquer item.** A meta não é a lista dos itens; é o motivo pelo qual eles serão escolhidos.

```
Ao final desta sprint, <papel> consegue <resultado observável>.
```

| Metas que não servem | Por quê |
|---|---|
| "Fazer as histórias 12, 15 e 18" | É a lista, não a meta |
| "Montar toda a estrutura do back-end" | Não entrega resultado a nenhum usuário |
| "Testar o agente de IA" | Descreve a ferramenta, não o produto |

**Autenticação fora desta sprint.** O scaffold simula um estudante autenticado. Histórias do território de identidade (cadastro, comprovação de e-mail, senha, recuperação de acesso) **não entram na Sprint 1**, mesmo que estejam no topo do backlog. Pule-as e registre isso na justificativa da seleção.

Exemplo em outro domínio (PedeJá): *"Ao final desta sprint, um cliente consegue ver o cardápio do dia e montar seu pedido no carrinho."*

> **Checkpoint 3** — A meta cabe em uma frase, nomeia um papel e descreve um resultado que alguém de fora da equipe consegue observar. Ela não depende de autenticação real.

---

### Etapa 4 — Selecionar as histórias (20 min)

1. Em **Boards › Backlogs**, abra **View options › Planning** para ver as sprints na lateral.
2. Percorra o backlog **do topo para baixo** e, para cada história, pergunte: *ela sustenta a meta?*
   - Sim → arraste-a para a `Sprint 1`.
   - Não → mantenha-a no backlog, mesmo que pareça fácil.
3. Antes de arrastar, confira os critérios de aceite. O agente vai usá-los como fonte, então cenários vagos precisam ser refinados agora e a mudança registrada em um comentário da história.
4. Selecione entre **2 e 4 histórias**, com pelo menos **uma fatia vertical completa**: tela, API e banco de dados.

> **Checkpoint 4** — Todas as histórias selecionadas sustentam a meta, têm cenários Gherkin verificáveis e nenhuma pertence ao território de identidade.

---

### Etapa 5 — Montar o esqueleto de tarefas (30 min)

O esqueleto é decisão da equipe. Antes de começar, salve o molde do Apêndice A no repositório, em `docs/moldes/task-pronta-para-agente.md`, para que o agente também possa consultá-lo.

Para cada história selecionada, crie as Tasks abaixo com o **+** da própria história em **Boards › Sprints › Backlog**. Assim elas já nascem vinculadas e na sprint correta.

| Prefixo no título | Tarefa | Quem executa | Esforço humano típico |
|---|---|---|---|
| `[ESP]` | Especificar o contrato da fatia: operação da API, dados de entrada e saída, erros esperados e o cenário que cada erro cobre | Integrante, com apoio do agente | 1h a 3h |
| `[BE]` | Implementar a fatia no back-end, com os testes de aceitação primeiro | Agente, supervisionado por um integrante | 2h a 6h |
| `[FE]` | Implementar a tela da fatia | Agente, supervisionado por um integrante | 2h a 6h |
| `[VER]` | Executar manualmente os cenários Gherkin na aplicação | Integrante que **não** supervisionou a implementação | 1h a 2h |
| `[REV]` | Revisar os pull requests da história por evidências | Integrante que **não** supervisionou a implementação | 1h a 2h |

- História sem tela dispensa `[FE]`.
- Uma história com muitos cenários pode ter mais de um `[BE]`, cada um com um conjunto coeso de cenários.
- Preencha o `Remaining Work` de cada Task com o esforço humano estimado. **Nenhuma Task acima de 8h.**
- Nesta etapa, o título e a estimativa bastam. A descrição completa vem na Etapa 6.

A equipe pode criar as Tasks à mão ou pedir ao agente, pela conexão `ado-planejamento`, que crie **exatamente** as Tasks decididas. Confira o resultado no board.

> **Checkpoint 5** — Toda história selecionada tem `[ESP]`, `[BE]`, `[VER]` e `[REV]`, e também `[FE]` quando tem tela. Todas as Tasks têm `Remaining Work` e nenhuma passa de 8h.

---

### Etapa 6 — Detalhar com o agente e auditar (45 min)

1. Com a conexão `ado-planejamento`, peça ao agente a proposta de descrição de cada Task `[BE]` e `[FE]`, seguindo o molde (prompt P1, Apêndice E). **O agente apenas propõe no chat; ninguém altera o work item ainda.** As seções de contrato ficam marcadas como "a definir na `[ESP]`".
2. Audite cada proposta com o checklist do Apêndice B. Para cada sugestão do agente, decida se ela é **aceita**, **modificada** ou **rejeitada**, e registre a decisão e o motivo em `docs/sprint-1-registro-ia.md`.
3. Só depois da auditoria, grave a descrição aprovada na Task, à mão ou pedindo ao agente que grave **o texto aprovado, sem mudanças**.
4. Peça ao agente uma crítica do plano completo (prompt P2). Ele deve apontar:
   - tarefas horizontais;
   - tarefas sem verificação;
   - tarefas grandes demais;
   - risco de violar fronteiras entre módulos;
   - cenários que nenhuma tarefa cobre.

   Registre as decisões da mesma forma.

> **Por que auditar, e não só aceitar.** O agente não conhece a disponibilidade da equipe nem as decisões ainda não registradas, e tende a propor tarefas por camada ("criar entidade", "criar controller"). A auditoria é o momento em que a equipe exerce o julgamento que esta atividade avalia.

> **Checkpoint 6** — Todas as Tasks `[BE]` e `[FE]` passam no checklist B. O registro de IA tem uma linha para cada sugestão avaliada, com a decisão e o motivo.

---

### Etapa 7 — Confrontar com a capacidade, registrar riscos e o Definition of Done (25 min)

**7.1 Capacidade.**

1. Em **Boards › Sprints › Taskboard**, abra **Work details** e compare a soma das horas com a capacidade.
2. Se ultrapassar, **devolva ao backlog a história de menor prioridade** e recalcule.
3. Não reduza números para o plano caber: isso falseia o plano em vez de ajustá-lo.

**7.2 Riscos.** Liste de três a cinco riscos concretos e a resposta prevista para cada um. Pelo menos um deve envolver o agente: cota esgotada, falhas repetidas em uma tarefa ou instabilidade da ferramenta.

**7.3 Definition of Done da história.** Ponto de partida obrigatório; a equipe pode acrescentar itens, não retirar.

- [ ] Cada cenário Gherkin coberto por `[BE]` tem um teste de aceitação automatizado com nome correspondente
- [ ] Os checks do pull request mostram o vermelho (commit dos testes) e o verde (commit da implementação)
- [ ] A sabotagem controlada está registrada no pull request, com pelo menos um teste falhando
- [ ] Os cenários foram executados manualmente na aplicação por quem não supervisionou a implementação (`[VER]`)
- [ ] Os pull requests foram revisados por outro integrante com o checklist D, e o CI está verde (testes e fronteiras)
- [ ] Todos os commits e pull requests citam `AB#<id>`
- [ ] As decisões sobre propostas do agente estão no registro de IA
- [ ] Todas as Tasks estão em `Closed`; a história foi movida para `Resolved` por quem executou e para `Closed` pelo guardião da qualidade

**7.4 Encerrar o planejamento.** Pare o servidor `ado-planejamento` (Caminho 1). No Caminho 2, que não tem modo somente leitura, siga a orientação do Apêndice G. A partir daqui, o agente só **lê** o board.

> **Checkpoint 7** — Nenhuma barra de capacidade ultrapassa o limite. Os riscos e o Definition of Done estão registrados. A conexão com permissão de escrita está desativada.

---

### Etapa 8 — Executar as tarefas (semanas 1 e 2)

#### 8.1 Antes de começar qualquer Task

1. Atribua a Task a quem vai supervisioná-la e mova-a para `Active`.
2. Crie um branch a partir do `main` atualizado, no formato `feat/AB<id>-descricao-curta`.
3. Inicie uma **sessão nova** do agente.

#### 8.2 Tarefa `[ESP]` — especificar o contrato

1. Com o apoio do agente, defina para a fatia:
   - a operação (verbo HTTP e rota);
   - os dados de entrada e de saída;
   - as respostas de erro.
2. Indique **qual cenário Gherkin cada resposta cobre**. Um cenário sem resposta correspondente indica contrato incompleto.
3. Grave o contrato na seção **Contrato** das Tasks `[BE]` e `[FE]` da história. A `[ESP]` não gera código nem pull request.
4. Feche a `[ESP]`.

#### 8.3 Tarefa `[BE]` — testes primeiro, depois a implementação

1. **Plano.** Peça ao agente que leia a Task e apresente o plano antes de tocar em qualquer arquivo (prompt P3). Confira o plano contra a Task: os arquivos estão dentro do escopo permitido? Há um teste por cenário? Aprove ou corrija.
2. **Testes primeiro.** Peça somente os testes de aceitação, no nível da API (prompt P4).
   - Rode o `<comando-de-verificacao>`. Os testes devem falhar **por asserção**: a funcionalidade ainda não existe.
   - Erro de compilação não conta como vermelho. Se isso acontecer, peça ao agente apenas o mínimo para compilar, sem nenhuma regra de negócio.
   - Faça o commit `test: cenarios de <historia> AB#<id>` e o push.
   - Abra o pull request como **rascunho** (*draft*) para que o CI rode e registre o vermelho.
3. **Implementação.** Peça a implementação mínima para os testes passarem, sem alterar os testes (prompt P5).
   - Rode o `<comando-de-verificacao>`.
   - Faça o commit `feat: <resultado> AB#<id>` e o push. O CI deve ficar verde.
4. **Sabotagem controlada.** Peça ao agente que introduza, sem commit, um único defeito na regra de negócio — nunca nos testes (prompt P6).
   - Rode os testes. **Pelo menos um deve falhar.** Registre qual.
   - Desfaça a alteração e confirme com `git status` que não sobrou nada.
   - Se nenhum teste falhar, os testes não verificam a regra: volte ao passo 2.
5. **Pull request.** Preencha o modelo e marque o pull request como pronto para revisão. O modelo deve conter:

```markdown
## Work items
AB#<task> · AB#<historia>

## O que muda
<duas ou três frases, com as palavras de quem supervisionou>

## Cenário → teste
| Cenário (Gherkin) | Teste |
|---|---|

## Vermelho → verde
- Commit dos testes: <hash> — check com falha
- Commit da implementação: <hash> — check verde

## Sabotagem controlada
- Defeito introduzido: <descrição>
- Testes que falharam: <nomes>

## Decisões sobre propostas do agente
<referência às linhas de docs/sprint-1-registro-ia.md>
```

#### 8.4 Tarefa `[FE]` — tela da fatia

O ciclo é o mesmo: plano, implementação, pull request. A diferença está na verificação:

- a tela deve permitir executar os cenários da história contra a API já integrada;
- a tela deve ser operável **só pelo teclado**;
- o pull request traz uma captura da tela em cada estado relevante: sucesso, erro e vazio.

Testes automatizados de componente são bem-vindos, mas não obrigatórios nesta sprint.

#### 8.5 Tarefas `[VER]` e `[REV]` — verificar e revisar

**`[VER]` — execução manual dos cenários.** Um integrante que não supervisionou a implementação:

1. sobe a aplicação com o comando do scaffold;
2. executa cada cenário Gherkin passo a passo;
3. registra o resultado em um comentário da história, nesta forma:

| Cenário | Resultado | Observação |
|---|---|---|

Se algum cenário falhar, crie um work item do tipo `Bug` vinculado à história. A história não fecha com bug aberto.

**`[REV]` — revisão por evidências.** O revisor:

1. aplica o checklist D;
2. pede ao agente que explique o diff (prompt P7);
3. escreve no pull request, **com as próprias palavras**, o que a mudança faz;
4. aprova ou pede mudanças;
5. integra só com a aprovação registrada e o CI verde.

Depois do merge, **uma pessoa** — nunca o agente — fecha as Tasks e zera o `Remaining Work`.

#### 8.6 Ponto de controle no meio da sprint (fim da semana 1, 15 min)

Mantenha o `Remaining Work` atualizado ao longo da sprint; sem isso, o gráfico não significa nada.

1. Abra o **burndown** da sprint (**Boards › Sprints › Analytics**) — o gráfico do trabalho restante ao longo dos dias — e compare-o com a linha ideal.
2. Se a equipe estiver claramente atrasada, decida **agora** qual história de menor prioridade volta ao backlog, para proteger a meta.
3. Registre a decisão na seção "Alterações de escopo" do planejamento.

#### 8.7 Protocolo de falha do agente

Uma **tentativa** é uma rodada em que o agente executa a Task e o `<comando-de-verificacao>` falha, ou o resultado viola o escopo da Task.

1. Depois de **três tentativas** sem sucesso, pare.
2. Descarte o branch.
3. Classifique a causa:

   | Código | Causa |
   |---|---|
   | A | Especificação ambígua ou incompleta |
   | B | Tarefa grande demais |
   | C | Dependência não declarada (outra Task, outro módulo, biblioteca) |
   | D | Limitação do ambiente ou da ferramenta |
   | E | Erro do agente com especificação adequada |

4. Corrija **a Task**, não o código. Registre a causa e a mudança em um comentário do work item e no registro de IA.
5. Recomece em uma sessão nova.
6. Se mais três tentativas falharem, registre um impedimento e leve-o ao docente ou à monitoria.

> **Nunca "resolva" uma falha removendo a verificação.** Desativar um teste, apagar uma verificação de fronteira ou editar o CI para passar transforma a evidência em mentira, e é tratado como ausência de entrega.

> **Checkpoint 8** — Todo pull request integrado tem as evidências do modelo, revisão registrada e CI verde. O board reflete o trabalho real: nenhuma Task fechada sem pull request integrado e nenhuma Task concluída ainda em `Active`.

---

### Etapa 9 — Verificar a meta (30 min, última aula da sprint)

1. **Demonstração.** Mostre a meta funcionando para alguém de fora da equipe (docente, monitoria ou outra equipe), seguindo os cenários das histórias concluídas.
2. **Situação de cada história.** Ou está em `Closed`, com o Definition of Done completo, ou **volta ao backlog**. Não existe "90% pronta".
3. **Encerramento.** Registre em `docs/sprint-1-encerramento.md`:
   - a meta foi atingida? Sim, parcialmente ou não, com a evidência;
   - histórias concluídas e devolvidas ao backlog;
   - Tasks planejadas × concluídas;
   - falhas do agente por causa (A a E);
   - três lições para a Sprint 2, sendo pelo menos uma sobre especificação.

> **Checkpoint 9** — Alguém de fora da equipe viu a meta funcionar ou entendeu, pela demonstração, por que ela não foi atingida. O board e o encerramento contam a mesma história.

---

## 6. Entregáveis

### 6.1 No Azure Boards

- `Sprint 1` com datas definidas e capacidade de **todos** os integrantes, com ausências marcadas
- Entre 2 e 4 histórias na `Sprint 1`, nenhuma do território de identidade
- Tasks de cada história no molde da Etapa 5, com descrição aprovada na auditoria e `Remaining Work` preenchido
- Commits e pull requests vinculados às Tasks (seção **Development** de cada work item)
- Estados coerentes com o trabalho: histórias em `Closed` ou devolvidas ao backlog ao final da sprint

### 6.2 No repositório `connexa-equipe-NN`

- **Código integrado no `main`**, exclusivamente por pull requests aprovados e com CI verde
- **Pull requests** com o modelo da Etapa 8.3 preenchido
- **`docs/sprint-1-planejamento.md`** com as seções:
  1. Meta da sprint
  2. Conta da capacidade, com as horas e o caminho de IA de cada integrante
  3. Justificativa da seleção, incluindo as histórias puladas e o motivo
  4. Esqueleto de tarefas de cada história
  5. Riscos e resposta prevista
  6. Definition of Done
  7. Registro da reunião de planejamento (data, duração e participantes)
  8. Alterações de escopo durante a sprint
- **`docs/sprint-1-registro-ia.md`** com duas tabelas:

```markdown
## Decisões sobre propostas do agente
| Data | Work item | Proposta do agente (resumo) | Decisão | Motivo |
|---|---|---|---|---|
|      | AB#      |                             | Aceita / Modificada / Rejeitada | |

## Falhas do agente
| Work item | Tentativas | Causa (A–E) | O que mudou na Task |
|---|---|---|---|
```

- **`docs/sprint-1-encerramento.md`**, conforme a Etapa 9
- **`docs/moldes/task-pronta-para-agente.md`**, cópia do Apêndice A, que pode ser adaptada pela equipe

### 6.3 Submissão no Microsoft Teams

Um único post da equipe, contendo:

- link do **Taskboard** da `Sprint 1`;
- link do repositório `connexa-equipe-NN`;
- links dos três arquivos de `docs/` desta sprint;
- captura de tela do **burndown** no último dia da sprint;
- nome completo de todos os integrantes.

---

## 7. Rubrica de avaliação (da equipe)

| Critério | Peso | Insuficiente | Adequado | Excelente |
|---|---:|---|---|---|
| **Planejamento e capacidade** | 15% | Meta ausente ou escrita como lista de itens; plano acima da capacidade | Meta no molde; plano dentro da capacidade, com a conta registrada | Ajustes de escopo feitos e justificados, antes ou durante a sprint |
| **Tarefas prontas para agente** | 20% | Tarefas genéricas ("fazer o back-end"), sem escopo nem forma de verificação | Todas as Tasks seguem o molde e passam no checklist B | A auditoria mostra propostas do agente modificadas ou rejeitadas por motivo técnico |
| **Testes como evidência** | 20% | Testes de aceitação ausentes ou sem evidência de vermelho | Um teste por cenário de back-end; vermelho → verde visível nos checks | Sabotagem registrada em todas as histórias; testes fracos apontados e corrigidos na revisão |
| **Revisão e integração** | 15% | Merge sem revisão ou com CI vermelho | Todos os pull requests revisados com o checklist D e integrados com CI verde | Revisões com perguntas e pedidos de mudança reais; pull requests pequenos e focados |
| **Rastreabilidade e board** | 10% | Commits ou pull requests sem `AB#`; board desatualizado | Todos com `AB#`; estados coerentes com o trabalho | Burndown coerente, com `Remaining Work` atualizado ao longo da sprint |
| **Registro de IA e protocolo de falha** | 10% | Registro ausente ou genérico | Decisões registradas com motivo; falhas classificadas | As falhas levaram a mudanças de especificação documentadas no work item |
| **Incremento e verificação da meta** | 10% | Nada demonstrável | Meta demonstrada, total ou parcialmente, com os cenários executados | Meta demonstrada a alguém de fora da equipe; encerramento com lições acionáveis |

> Quantidade de código não é critério. Os critérios avaliam **como** o incremento foi especificado, verificado e integrado.

---

## 8. Checklist de entrega

- [ ] Checkpoints 0 a 9 verificados pela equipe
- [ ] `Sprint 1` com datas, capacidade, histórias e Tasks no molde
- [ ] Nenhuma história do território de identidade na sprint
- [ ] Todo código no `main` entrou por pull request aprovado e com CI verde
- [ ] Todo pull request de `[BE]` tem a tabela cenário → teste, o vermelho → verde e a sabotagem
- [ ] Todo commit e pull request cita `AB#<id>`, sem `Fixes`
- [ ] Os três arquivos de `docs/` desta sprint estão no `main`
- [ ] O post no Teams contém todos os links e a captura do burndown
- [ ] O docente tem acesso de leitura à organização GitHub e ao projeto no Azure DevOps

---

## 9. Erros frequentes

| Erro | Consequência | Correção |
|---|---|---|
| Pedir ao agente "implemente a história inteira" | Pull request enorme, impossível de revisar; cota consumida de uma vez | Uma Task por sessão, no tamanho do molde |
| Especificar só no chat do agente | O trabalho desaparece com a sessão; ninguém mais consegue continuar | A especificação vive na Task; o chat é descartável |
| Aprovar o plano do agente sem conferir contra a Task | Arquivos fora do módulo e escopo extra | Conferir os arquivos permitidos e os cenários antes de aprovar |
| Implementar antes dos testes | Sem evidência de vermelho; o teste pode estar só confirmando o código | Primeiro commit do branch somente com os testes |
| Aceitar erro de compilação como vermelho | Não prova que o teste verifica o comportamento | O vermelho precisa ser uma falha de asserção |
| Deixar o agente alterar os testes para passar | O teste deixa de verificar o cenário | Rejeitar; testes só mudam com justificativa registrada |
| Desativar teste ou verificação de fronteira para o CI passar | Evidência falsa | Nunca; aplicar o protocolo de falha |
| Insistir com o agente sem limite | Cota e tempo perdidos | Três tentativas; depois, corrigir a especificação |
| Revisar lendo o código "por cima" e aprovar | A revisão vira carimbo | Checklist D e explicação do diff com as próprias palavras |
| Usar `Fixes AB#<id>` | Work item fechado automaticamente, sem Definition of Done | Usar apenas `AB#<id>`; estados são movidos por pessoas |
| Manter a conexão com escrita ativa durante a execução | O agente altera o board | Somente `ado-leitura` a partir da Etapa 8 |
| Sprint só de back-end | Nada demonstrável a um usuário | Pelo menos uma fatia vertical completa |
| Incluir história de identidade | Fora do escopo desta sprint | Pular e registrar na justificativa da seleção |
| Colar dados pessoais reais em prompts ou dados de teste | Exposição de dados (LGPD) | Usar apenas dados fictícios |

---

## 10. Material de apoio

- **Exemplo de referência — Sprint 1 do PedeJá com agente** (`Exemplo_Referencia_Sprint1_PedeJa.md`): forma e nível esperados, em outro domínio
- Roteiro **RA-01 — Construção do Product Backlog** e o exemplo de backlog do PedeJá
- Apresentação **Arquiteturas de Software** (Parte 5) e o ADR-001 da equipe
- Material da aula de testes de software
- Documentação oficial:
  - Azure Boards e GitHub: <https://learn.microsoft.com/azure/devops/boards/github/>
  - Servidor MCP remoto do Azure DevOps: <https://learn.microsoft.com/azure/devops/mcp-server/remote-mcp-server>
  - Servidor MCP local do Azure DevOps: <https://github.com/microsoft/azure-devops-mcp/blob/main/docs/GETTINGSTARTED.md>
  - MCP no Codex: <https://developers.openai.com/codex/mcp>

---

## Apêndice A — Molde de Task pronta para agente

```markdown
Título: [BE] <verbo> <resultado observável> — <história, em poucas palavras>

## Objetivo
<Uma frase: o que passa a funcionar quando esta Task terminar.>

## História e cenários
História: AB#<id da história>
Cenários cobertos por esta Task: <nomes exatos dos cenários Gherkin>
Cenários fora desta Task: <quais e por quê>

## Contrato  (preenchido pela Task [ESP])
Operação: <verbo HTTP> <rota>
Entrada: <campos, tipos e obrigatoriedade>
Saída: <campos>
Erros: <código de resposta> quando <situação> → cenário "<nome>"

## Escopo
Pode alterar: <módulo e pastas>
Pode usar sem alterar: <API pública de outro módulo, se necessária>
Não pode alterar: testes existentes, CI, configuração de fronteiras,
                  dependências do projeto, outros módulos

## Verificação
Comando: <comando-de-verificacao>
Pronto quando: os testes de aceitação dos cenários acima passam
e nenhuma verificação existente falha.

## Fora de escopo
<O que o agente não deve fazer, mesmo que pareça útil.>
```

Para Tasks `[FE]`, a seção **Verificação** passa a ser: *"Pronto quando a tela permite executar os cenários <nomes> contra a API integrada, é operável só pelo teclado e exibe os estados de sucesso, erro e vazio."*

---

## Apêndice B — Checklist de auditoria de Task

- [ ] O objetivo cabe em uma frase e descreve um resultado observável
- [ ] A Task cita a história e nomeia os cenários que cobre
- [ ] O contrato está preenchido (`[BE]` e `[FE]`, depois da `[ESP]`)
- [ ] O escopo se limita a um módulo do back-end ou à pasta da funcionalidade no front-end
- [ ] A lista do que não pode ser alterado inclui testes existentes, CI e dependências
- [ ] O comando e a condição de pronto estão explícitos
- [ ] A Task é vertical: entrega comportamento verificável, e não "criar a camada X"
- [ ] O esforço humano estimado está entre 1h e 8h
- [ ] Nada depende de autenticação real
- [ ] Um integrante que não escreveu a Task entende o que será entregue lendo **apenas** o work item

---

## Apêndice C — Checklist de teste ruim (revisão da aula de testes)

Um teste deve ser questionado quando:

- não tem asserção, ou a asserção passa em qualquer situação;
- verifica a simulação (*mock*) em vez do comportamento;
- verifica só parte do resultado esperado (por exemplo, o código de resposta, mas não o estado que deveria mudar ou permanecer igual);
- tem nome que não corresponde a nenhum cenário — ou existe cenário sem teste;
- verifica detalhes internos em vez do resultado observável descrito no cenário;
- foi alterado para passar depois de ter falhado;
- está marcado como ignorado ou desativado;
- ficou vermelho por erro de compilação, e não por asserção;
- não falhou na sabotagem controlada.

---

## Apêndice D — Checklist de revisão por evidências

- [ ] **Escopo.** O diff só toca o que a Task permite; nada em testes existentes, CI, configuração de fronteiras ou dependências
- [ ] **Rastreabilidade.** Título ou descrição com `AB#<task>` e `AB#<historia>`; o vínculo aparece no work item
- [ ] **Tamanho.** O pull request corresponde a uma única Task
- [ ] **Cenário → teste.** Todos os cenários da Task têm teste com nome correspondente (Apêndice C)
- [ ] **Vermelho → verde.** Os checks mostram a falha no commit dos testes e o sucesso no commit da implementação
- [ ] **Sabotagem.** Registrada, com pelo menos um teste falhando
- [ ] **CI.** Verde, incluindo a verificação de fronteiras entre módulos
- [ ] **Compreensão.** O revisor escreveu, com as próprias palavras, o que a mudança faz
- [ ] **Dados.** Nenhum segredo, token ou dado pessoal real no código, nos testes ou nos prompts
- [ ] **Front-end** (quando houver). Capturas dos estados de sucesso, erro e vazio; operação pelo teclado verificada

---

## Apêndice E — Prompts de referência

Adapte as palavras, mas mantenha a intenção. Substitua `<id>` pelo número real do work item.

**P1 — Detalhar uma Task** (conexão `ado-planejamento`, Etapa 6)
> Leia a User Story AB#<id> e a Task AB#<id> do projeto Connexa. Seguindo o molde em `docs/moldes/task-pronta-para-agente.md` e as regras do `AGENTS.md`, proponha o texto da descrição desta Task. Deixe a seção Contrato como "a definir na [ESP]". **Não altere nenhum work item**: apenas mostre a proposta e aponte qualquer ambiguidade nos cenários.

**P2 — Criticar o plano** (conexão `ado-planejamento`, Etapa 6)
> Leia todas as Tasks da Sprint 1 do projeto Connexa e as histórias a que pertencem. Avalie o plano contra o molde e o `AGENTS.md` e aponte: tarefas organizadas por camada técnica, tarefas sem forma de verificação, tarefas grandes demais, risco de violar fronteiras entre módulos e cenários que nenhuma tarefa cobre. **Não altere nada.**

**P3 — Planejar a execução** (conexão `ado-leitura`, Etapa 8)
> Leia a Task AB#<id>. Antes de alterar qualquer arquivo, apresente seu plano: os arquivos que vai criar ou alterar, um teste por cenário (nome do teste → cenário) e o comando de verificação. Aguarde a minha aprovação.

**P4 — Testes primeiro**
> Escreva somente os testes de aceitação, no nível da API, para os cenários listados na Task AB#<id>. Não implemente a funcionalidade. Os testes devem compilar e falhar por asserção. Rode `<comando-de-verificacao>` e mostre o resultado.

**P5 — Implementar**
> Implemente o mínimo necessário para que os testes da Task AB#<id> passem, respeitando o escopo da Task e o `AGENTS.md`. Não altere os testes. Rode `<comando-de-verificacao>` e mostre o resultado.

**P6 — Sabotagem controlada**
> Sem fazer commit, introduza um único defeito na regra de negócio coberta pela Task AB#<id> — não altere os testes. Rode os testes e diga quais falharam. Em seguida, desfaça a alteração.

**P7 — Explicar o diff** (revisor)
> Explique, para alguém que conhece pouco o framework, o que este pull request muda, arquivo por arquivo, e qual cenário cada teste verifica. Aponte qualquer alteração fora do escopo da Task AB#<id>.

---

## Apêndice F — Caminho 1: GitHub Copilot com o servidor MCP remoto

**Requisitos:** GitHub Copilot ativo na conta GitHub do integrante (plano Copilot Student ou gratuito); VS Code com a extensão GitHub Copilot Chat; conta institucional com acesso ao projeto `Connexa`.

1. Abra o arquivo `.vscode/mcp.json` fornecido pelo scaffold e substitua `<organizacao-azure-devops>` pelo nome da organização. O conteúdo esperado é:

```json
{
  "servers": {
    "ado-planejamento": {
      "type": "http",
      "url": "https://mcp.dev.azure.com/<organizacao-azure-devops>",
      "headers": { "X-MCP-Toolsets": "wit,work" }
    },
    "ado-leitura": {
      "type": "http",
      "url": "https://mcp.dev.azure.com/<organizacao-azure-devops>",
      "headers": { "X-MCP-Toolsets": "wit,work", "X-MCP-Readonly": "true" }
    }
  },
  "inputs": []
}
```

2. Salve o arquivo e inicie o servidor `ado-leitura`, pela visão de servidores MCP do VS Code ou pelo botão **Start** exibido no próprio arquivo.
3. Quando solicitado, autentique-se com a **conta institucional**.
4. Abra o Copilot Chat no modo **Agent** e confira, no seletor de ferramentas, que as ferramentas do Azure DevOps aparecem.
5. Faça o teste: *"Liste os projetos da minha organização no Azure DevOps."*
6. Nas Etapas 5 e 6, inicie também o `ado-planejamento`. Pare-o ao concluir a Etapa 7.

**Boas práticas**

- Não ative a aprovação automática de ferramentas: leia cada chamada antes de aprovar.
- O arquivo de instruções do repositório é lido automaticamente pelo agente; não é preciso colá-lo no chat.
- Não grave tokens nem senhas em `mcp.json`. A autenticação é feita pelo navegador.

**Problemas comuns**

| Sintoma | O que fazer |
|---|---|
| A autenticação pede aprovação de um administrador | Avise o docente — a política da instituição pode exigir consentimento — e use o Caminho 2 enquanto isso |
| As ferramentas do Azure DevOps não aparecem | Confira se o servidor está iniciado e se o chat está no modo Agent |
| O agente responde sem dados | Confira o nome da organização no arquivo e se sua conta tem acesso ao projeto |
| A cota do Copilot acabou | Outro integrante assume a Task, ou use o Caminho 2 |

---

## Apêndice G — Caminho 2: Codex com o servidor MCP local

**Requisitos:** conta ChatGPT (o plano gratuito inclui uso limitado do Codex); extensão Codex no VS Code com sessão iniciada; Node.js 20 ou superior; conta institucional com acesso ao projeto `Connexa`.

> O Codex ainda não consegue autenticar no servidor MCP remoto do Azure DevOps. Por isso, ele usa o servidor **local**, que roda na sua máquina via `npx`.

1. **Configure o servidor.** Escolha uma das formas:
   - **Pelo projeto:** se o scaffold forneceu `.codex/config.toml`, substitua `<organizacao-azure-devops>` e marque o projeto como confiável quando o Codex perguntar. A configuração de projeto só vale para projetos confiáveis.
   - **Pelo terminal:**
     ```bash
     codex mcp add azure-devops -- npx -y @azure-devops/mcp <organizacao-azure-devops> -d core work work-items
     ```
   - **Pelo arquivo do usuário:** na extensão, abra **MCP settings › Open config.toml** e acrescente:
     ```toml
     [mcp_servers.azure-devops]
     command = "npx"
     args = ["-y", "@azure-devops/mcp", "<organizacao-azure-devops>", "-d", "core", "work", "work-items"]
     ```
2. Reinicie o Codex. No primeiro uso de uma ferramenta do Azure DevOps, o navegador abrirá para login: use a **conta institucional**.
3. Faça o teste: *"Liste os projetos da minha organização no Azure DevOps."*

**Menor privilégio no Caminho 2.** O servidor local não tem um modo somente leitura equivalente ao do remoto. Por isso:

- use o modo do Codex que **pede aprovação** antes de executar comandos e chamadas de ferramenta — nunca o modo de acesso total (*full access*);
- a partir da Etapa 8, **recuse** qualquer chamada que crie ou altere work items.

**Problemas comuns**

| Sintoma | O que fazer |
|---|---|
| No Windows, o servidor não inicia | Troque para `command = "cmd"` e `args = ["/c", "npx", "-y", "@azure-devops/mcp", "<organizacao-azure-devops>", "-d", "core", "work", "work-items"]` |
| `npx` não é reconhecido | Instale o Node.js 20 ou superior e reabra o VS Code |
| O Codex informa limite de uso atingido | O plano gratuito tem cota em janelas de tempo; outro integrante assume a Task ou use o Caminho 1 |
| Erro do *sandbox* do Codex na máquina do laboratório | Comunique o docente; máquinas sem permissão de administrador podem exigir outro modo de execução |

**Privacidade.** Não cole dados pessoais reais em prompts e revise os controles de dados da sua conta ChatGPT.

---

*Roteiro de atividade — Disciplina de Engenharia de Software — Projeto Connexa.*
