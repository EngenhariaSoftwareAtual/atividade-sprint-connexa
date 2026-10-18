# Atividade de Sprint — Roteiro
## Sprint 1 do Connexa: planejamento e execução com agente de IA

**Disciplina de Engenharia de Software** · Prof. Claudio Nunes
**Modalidade:** em equipe (4 a 5 integrantes) · **Duração:** duas aulas de laboratório e uma sprint de duas semanas
**Ferramentas:** Azure Boards (processo *Agile*), GitHub, VS Code com agente de IA (GitHub Copilot ou Codex) conectado ao Azure Boards por MCP
**Submissão:** Microsoft Teams, uma entrega ao fim de cada parte

---

### Convenções deste documento

| Marcador | Significado |
|---|---|
| `<organizacao-azure-devops>` | Organização da equipe no Azure DevOps, criada na Atividade de Requisitos com a conta institucional. O nome é escolhido pela equipe |
| `<organizacao-github>` | Organização da equipe no GitHub, criada na Etapa 1. O nome é escolhido pela equipe |
| `<repositorio-da-equipe>` | Repositório de produto da equipe (front-end, back-end e documentação), público, criado na Etapa 2 a partir do template. O nome é escolhido pela equipe; sugestão: `connexa-<nome-da-equipe>` |
| `<id>` | Número de um work item no Azure Boards — em commits e pull requests, escrito como `AB#<id>` |
| `<comando-de-verificacao>` | Comando único que roda localmente tudo o que o CI roda, documentado no `README` do template |
| **o agente** | O assistente de IA que cada integrante usa no VS Code — GitHub Copilot ou Codex. Todas as etapas valem para os dois |

> Os nomes das organizações e do repositório são livres, mas não devem mudar depois de criados: links, conexões e configurações dependem deles. O projeto no Azure DevOps continua se chamando exatamente `Connexa`.

---

## 1. Cenário

O Product Backlog do Connexa está pronto (Atividade de Requisitos). Começa agora a primeira sprint: duas semanas para transformar histórias do topo do backlog em um incremento que alguém de fora da equipe consiga usar e verificar.

A atividade tem duas partes, cada uma com a sua entrega:

- **Parte 1 — Preparação do ambiente (Aula 1).** A equipe cria a organização no GitHub, o repositório a partir do template da solução de arquitetura escolhida, a conexão entre o Azure Boards e o GitHub e a conexão do agente com o Azure Boards.
- **Parte 2 — Planejamento, execução e encerramento (Aula 2 e as duas semanas da sprint).** A equipe planeja a sprint, executa as tarefas com o agente e verifica a meta.

Nesta sprint, **o código é escrito por um agente de IA**. Isso não dispensa a equipe do trabalho — muda o trabalho. Cabe à equipe decidir o que cabe na sprint, transformar cada tarefa em uma especificação que o agente consiga executar, exigir testes antes do código, conferir as evidências e decidir o que entra no `main`.

O agente lê as tarefas diretamente do Azure Boards por meio de um servidor **MCP** (*Model Context Protocol*), o protocolo que permite a um assistente de IA consultar ferramentas externas. A consequência prática é imediata: o que estiver mal especificado no work item vira código errado em minutos.

> **Foco da atividade.** Não a quantidade de código, e sim práticas de engenharia: planejamento por capacidade, decomposição, especificação, verificação, revisão, rastreabilidade e integração. Uma história concluída com todas as evidências vale mais do que três histórias que ninguém consegue demonstrar.

---

## 2. Objetivos de aprendizagem

| Nível (Bloom) | Objetivo |
|---|---|
| Entender | Explicar a divisão de papéis entre equipe e agente e por que a qualidade da especificação determina a qualidade do resultado |
| Aplicar | Preparar o repositório da equipe e conectar Azure Boards, GitHub e o agente |
| Aplicar | Configurar a sprint e a capacidade e escrever tarefas prontas para agente, com escopo, critérios e forma de verificação explícitos |
| Analisar | Confrontar o plano com a capacidade real da equipe e identificar o excesso antes do início da sprint |
| Avaliar | Auditar tarefas, testes e pull requests produzidos com IA a partir de evidências, aceitando, modificando ou rejeitando cada proposta com justificativa |
| Criar | Produzir um incremento verificável, rastreado do work item até o código integrado |

---

## 3. Pré-requisitos

### 3.1 Atividades anteriores

- [ ] Atividade de Requisitos entregue e corrigida: backlog ordenado, com `Story Points`, Tags MoSCoW e critérios de aceite em Gherkin em todas as histórias
- [ ] Organização do Azure DevOps criada com a conta institucional e ligada ao **Microsoft Entra ID** da instituição. Confira em **Organization settings › Microsoft Entra**: a página deve mostrar o diretório da instituição. A conexão do agente com o Azure Boards (Caminho 1) só funciona nessa condição
- [ ] Aula de testes de software concluída: níveis de teste, ciclo vermelho → verde, checklist de teste ruim e sabotagem controlada
- [ ] Solução de arquitetura escolhida pela equipe, conforme a apresentação **Arquiteturas de Software**

### 3.2 Contas e ferramentas de cada integrante

- [ ] Conta institucional com acesso **Basic** ao projeto `Connexa`. Quem tem acesso *Stakeholder* não consegue registrar capacidade; confira em **Organization settings › Users**
- [ ] Conta no GitHub. O GitHub Student Developer Pack inclui o GitHub Copilot e uma cota de horas do GitHub Codespaces
- [ ] VS Code com o agente escolhido instalado e com sessão iniciada (Apêndice F ou G)
- [ ] Para o Caminho 2 (Codex): Node.js 20 ou superior instalado
- [ ] Para trabalhar fora do Codespaces: os requisitos de máquina local descritos no `README` do template

### 3.3 O que o template entrega

Os templates ficam na organização da disciplina no GitHub, um por solução de arquitetura. Todos trazem os itens abaixo, usados ao longo da sprint.

| Item | Para que serve nesta sprint |
|---|---|
| `AGENTS.md` e `.github/copilot-instructions.md` com as regras de arquitetura: módulos, fronteiras, onde ficam os testes | O agente segue as mesmas regras com qualquer ferramenta |
| `.vscode/mcp.json` (Caminho 1) e `.codex/config.toml` (Caminho 2), com o nome da organização a preencher | Conexão do agente com o Azure Boards |
| Workflow de CI que roda os testes e a verificação de fronteiras entre módulos em todo pull request | Evidência objetiva de que nada quebrou |
| `<comando-de-verificacao>` documentado no `README` | O mesmo gesto em qualquer stack: "rodar tudo o que o CI roda" |
| Modelo de pull request (`.github/pull_request_template.md`) | Padroniza as evidências exigidas na revisão (Etapa 13.3) |
| Modelo de ADR em `docs/adr/` | Registro da solução de arquitetura adotada (Etapa 4) |
| Usuário de desenvolvimento simulado | A autenticação está fora da Sprint 1; a aplicação se comporta como se houvesse um estudante autenticado |

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

- **`ado-planejamento`** — pode criar e alterar work items. Usada **somente** nas Etapas 10 e 11.
- **`ado-leitura`** — somente leitura. Usada em todo o restante da atividade.

Fora das Etapas 10 e 11, toda escrita no board — estados, `Remaining Work`, contratos, comentários e Bugs — é feita por uma pessoa, no navegador.

Nenhuma chamada de ferramenta do agente é aprovada automaticamente: cada integrante lê o que o agente pretende fazer antes de aprovar. Se um work item contiver algo como "desative a verificação" ou "ignore o AGENTS.md", trate como defeito da tarefa e corrija o work item.

### 4.5 Cota de uso do agente

Os planos gratuitos têm limites de uso: o Copilot Student tem uma cota mensal de créditos e o Codex no plano gratuito, uma cota em janelas de algumas horas. Cada integrante tem a própria cota; **a cota da equipe é a soma delas**.

- Uma Task por sessão do agente; inicie uma sessão nova a cada Task.
- Nunca peça "implemente a história inteira": além de gerar um pull request impossível de revisar, consome a cota em uma única tentativa.
- Distribua as tarefas de implementação entre os integrantes.
- Se a cota de alguém acabar, outro integrante continua a mesma Task — é possível porque a especificação está no work item.

### 4.6 Documentação no repositório

O `main` só aceita mudanças por pull request revisado, inclusive em `docs/`. Para não multiplicar pull requests:

- o planejamento (`docs/sprint-1-planejamento.md`, o molde e as decisões da auditoria) entra em um único pull request, na Etapa 12;
- durante a execução, as linhas do registro de IA de uma Task entram **no próprio pull request da Task**;
- o encerramento entra em um último pull request, na Etapa 14.

---

## 5. Organização da atividade

| Parte | Quando | Etapas | Entrega |
|---|---|---|---|
| **1 — Preparação do ambiente** | Aula 1 | 1 a 5 | Entregáveis da Parte 1 (seção 6) |
| **2 — Planejamento** | Aula 2; o que não couber é concluído em reunião da equipe até o segundo dia da sprint | 6 a 12 | — |
| **2 — Execução** | Semanas 1 e 2 da sprint, com ponto de controle no fim da semana 1 (13.6) | 13 | — |
| **2 — Encerramento** | Último dia da sprint | 14 | Entregáveis da Parte 2 (seção 7) |

> A execução (Etapa 13) só começa depois que o **Checkpoint 12** estiver verificado. Os tempos indicados são estimativas.

---

# Parte 1 — Preparação do ambiente (Aula 1)

### Etapa 1 — Criar a organização da equipe no GitHub (15 min)

Um integrante executa; os demais aceitam o convite em seguida.

1. No GitHub, abra o menu do perfil › **Your organizations › New organization** e escolha o plano **Free**.
2. Informe o nome escolhido pela equipe para `<organizacao-github>` e, como e-mail de contato, o e-mail institucional. Indique que a organização pertence à sua conta pessoal.
3. Em **People › Invite member**, convide os demais integrantes. Torne pelo menos mais um integrante **Owner**, para que a organização não dependa de uma única pessoa.
4. Em **Settings › Member privileges › Base permissions**, selecione **Write**, para que todos possam criar branches e abrir pull requests.

> **Checkpoint 1** — Todos os integrantes aceitaram o convite e aparecem em **People**; pelo menos dois são Owners.

---

### Etapa 2 — Criar o repositório a partir do template (20 min)

1. Abra o template correspondente à solução de arquitetura escolhida pela equipe:

   | Solução | Template |
   |---|---|
   | Java | [`connexa-modelo-java`](https://github.com/EngenhariaSoftwareAtual/connexa-modelo-java) |
   | .NET | [`connexa-modelo-dotnet`](https://github.com/EngenhariaSoftwareAtual/connexa-modelo-dotnet) |
   | Node.js | [`connexa-modelo-node`](https://github.com/EngenhariaSoftwareAtual/connexa-modelo-node) |

2. Selecione **Use this template › Create a new repository**.
3. Em **Owner**, escolha `<organizacao-github>`. Informe o nome `<repositorio-da-equipe>` e marque **Public**.
4. Cada integrante abre o ambiente de trabalho seguindo a seção "Começar a trabalhar" do `README` do repositório — o GitHub Codespaces é o caminho recomendado — e roda o `<comando-de-verificacao>`.

> **Checkpoint 2** — O repositório é público, pertence a `<organizacao-github>` e foi criado a partir do template da solução escolhida. Todos os integrantes rodaram o `<comando-de-verificacao>` sem falhas.

---

### Etapa 3 — Conectar o Azure Boards ao repositório (15 min)

Esta etapa exige um integrante que seja administrador do projeto `Connexa` no Azure DevOps e Owner de `<organizacao-github>`.

1. No Azure DevOps, abra **Project Settings › Boards › GitHub connections** e selecione **Connect your GitHub account**.
2. Escolha `<organizacao-github>` e marque o repositório `<repositorio-da-equipe>`.
3. O GitHub pedirá a aprovação do aplicativo **Azure Boards** na organização. Aprove apenas para `<repositorio-da-equipe>`.

| Sintoma | O que fazer |
|---|---|
| A lista de repositórios aparece vazia | No GitHub, abra **Settings › OAuth app policy** da organização e permita o acesso do Azure Boards |
| O Azure DevOps recusa a conexão por falta de permissão | Quem conecta precisa ser administrador do projeto `Connexa` |

> **Checkpoint 3** — `<repositorio-da-equipe>` aparece em **GitHub connections**.

---

### Etapa 4 — Preparar o repositório e registrar o ADR-001 (40 min)

Esta etapa também testa, de ponta a ponta, o vínculo entre work item, commit e pull request.

1. No Azure Boards, crie uma Task chamada `Preparar o repositório da equipe` (**Boards › Work items › New Work Item › Task**), **fora** da Sprint 1. Anote o número.
2. Crie o branch `chore/AB<id>-preparar-repositorio` a partir do `main`.
3. Em `.vscode/mcp.json` e `.codex/config.toml`, substitua `<organizacao-azure-devops>` pelo nome da organização no Azure DevOps.
4. Registre o **ADR-001** em `docs/adr/`, a partir do modelo da pasta: a solução de arquitetura e a stack adotadas, o contexto e o motivo da escolha.
5. Faça o commit `docs: ADR-001 e configuracao do MCP AB#<id>`, o push e abra um pull request com `AB#<id>` na descrição. O CI roda pela primeira vez.
6. **Proteja o `main`.** Em **Settings › Rules › Rulesets › New branch ruleset**, crie uma regra ativa para o branch padrão que:
   - exija pull request antes do merge, com **1 aprovação**;
   - exija os checks do CI listados no `README` do template — eles aparecem na lista depois da execução do passo 5;
   - bloqueie *force push* e a exclusão do branch;
   - não tenha ninguém na lista de exceções (*bypass list*).
7. Outro integrante revisa o pull request e o aprova. Integre-o depois do CI verde.
8. Abra a Task no Azure Boards e confira, na seção **Development**, o vínculo com o commit e o pull request. Feche a Task.

> **Atenção ao vínculo.** Escreva apenas `AB#<id>` em commits e pull requests. Palavras como `Fixes AB#<id>` podem mudar o estado do work item automaticamente no merge; nesta atividade, os estados são movidos por pessoas.

> **Checkpoint 4** — O ADR-001 e a configuração do MCP estão no `main`. O pull request aparece vinculado à Task. O `main` não aceita integração sem pull request aprovado e CI verde.

---

### Etapa 5 — Conectar o agente ao Azure Boards (30 min)

1. Cada integrante atualiza o próprio ambiente com o `main` e segue o Apêndice F (GitHub Copilot) ou o Apêndice G (Codex). Integrantes da mesma equipe podem usar caminhos diferentes.
2. **Teste de fumaça.** Com a conexão `ado-leitura` (ou, no Caminho 2, aprovando apenas chamadas de leitura), cada integrante pede ao agente:
   > Liste as User Stories do projeto Connexa na ordem do backlog, com ID, título e Story Points. Não altere nada.

   Compare a resposta com o que aparece em **Boards › Backlogs**.
3. Registre, para cada integrante, o caminho de IA usado e o resultado do teste.

> **Checkpoint 5** — Cada integrante obteve do agente dados reais do board, iguais aos exibidos no Azure Boards.

---

## 6. Entregáveis da Parte 1

### 6.1 No GitHub e no Azure Boards

- `<organizacao-github>` com todos os integrantes e base permission **Write**
- `<repositorio-da-equipe>` público, criado a partir do template da solução escolhida
- ADR-001 e configuração do MCP no `main`, integrados por pull request aprovado e com CI verde
- Regra de proteção do `main` ativa
- Task `Preparar o repositório da equipe` fechada, com o commit e o pull request na seção **Development**

### 6.2 Submissão no Microsoft Teams

Um único post da equipe, contendo:

- link de `<repositorio-da-equipe>`;
- link do pull request da Etapa 4;
- captura de tela da seção **Development** da Task da Etapa 4;
- captura de tela da regra de proteção do `main`;
- tabela com o nome completo de cada integrante, o caminho de IA (Copilot ou Codex) e o resultado do teste de fumaça.

### 6.3 Checklist da Parte 1

- [ ] Checkpoints 1 a 5 verificados pela equipe
- [ ] Nenhum commit direto no `main` depois da criação do repositório
- [ ] O post no Teams contém todos os links e capturas

---

# Parte 2 — Planejamento, execução e encerramento (Aula 2 e as duas semanas da sprint)

### Etapa 6 — Configurar a sprint na ferramenta (15 min)

1. **Project Settings › Boards › Project configuration › Iterations**: abra `Sprint 1` e informe as datas de início e de fim (duas semanas).
2. **Project Settings › Boards › Team configuration › Iterations**: confirme que `Sprint 1` está na lista de iterações da equipe.
3. **Project Settings › Boards › Team configuration › Working days**: marque os dias em que a equipe efetivamente trabalha. A capacidade e o burndown são calculados sobre esses dias.

> **Checkpoint 6** — `Sprint 1` aparece no seletor de sprints com as datas corretas, e os dias úteis da equipe estão configurados.

---

### Etapa 7 — Calcular e registrar a capacidade de esforço humano (20 min)

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
Alvo da primeira sprint (75%) ...................  33h
```

**Regra da primeira sprint:** sem histórico, planeje entre **70% e 80%** da capacidade de planejamento. A primeira sprint com agente costuma consumir mais tempo de verificação do que a equipe imagina.

**Registre o alvo na ferramenta.** Em **Boards › Sprints › Capacity**, cadastre cada integrante e informe as **horas por dia** que correspondem à parte dele no **alvo**, e não na capacidade bruta: horas do alvo do integrante ÷ dias úteis da sprint, arredondado para baixo. No exemplo, 33h ÷ 5 integrantes ÷ 10 dias úteis ≈ **0,6 h por dia**. Marque também os dias de ausência já conhecidos. Assim, as barras de capacidade da Etapa 12 comparam o plano com o alvo.

> **Checkpoint 7** — A equipe tem um número único de horas de alvo, com a conta registrada por escrito, e a aba *Capacity* mostra todos os integrantes com as horas por dia correspondentes.

---

### Etapa 8 — Escrever a meta da sprint (15 min, sem ferramenta)

**Escreva a meta antes de escolher qualquer item.** A meta não é a lista dos itens; é o motivo pelo qual eles serão escolhidos.

```
Ao final desta sprint, <papel> consegue <resultado observável>.
```

| Metas que não servem | Por quê |
|---|---|
| "Fazer as histórias 12, 15 e 18" | É a lista, não a meta |
| "Montar toda a estrutura do back-end" | Não entrega resultado a nenhum usuário |
| "Testar o agente de IA" | Descreve a ferramenta, não o produto |

**Autenticação fora desta sprint.** O template simula um estudante autenticado. Histórias do território de identidade (cadastro, comprovação de e-mail, senha, recuperação de acesso) **não entram na Sprint 1**, mesmo que estejam no topo do backlog. Pule-as e registre isso na justificativa da seleção.

Exemplo em outro domínio (PedeJá): *"Ao final desta sprint, um cliente consegue ver o cardápio do dia e montar seu pedido no carrinho."*

> **Checkpoint 8** — A meta cabe em uma frase, nomeia um papel e descreve um resultado que alguém de fora da equipe consegue observar. Ela não depende de autenticação real.

---

### Etapa 9 — Selecionar as histórias (20 min)

1. Em **Boards › Backlogs**, abra **View options › Planning** para ver as sprints na lateral.
2. Percorra o backlog **do topo para baixo** e, para cada história, pergunte: *ela sustenta a meta?*
   - Sim → arraste-a para a `Sprint 1`.
   - Não → mantenha-a no backlog, mesmo que pareça fácil.
3. Antes de arrastar, confira os critérios de aceite. O agente vai usá-los como fonte, então cenários vagos precisam ser refinados agora e a mudança registrada em um comentário da história.
4. Selecione entre **2 e 4 histórias**, com pelo menos **uma fatia vertical completa**: tela, API e banco de dados.

> **Checkpoint 9** — Todas as histórias selecionadas sustentam a meta, têm cenários Gherkin verificáveis e nenhuma pertence ao território de identidade.

---

### Etapa 10 — Montar o esqueleto de tarefas (30 min)

O esqueleto é decisão da equipe.

**Prepare a documentação do planejamento.** Crie uma Task `Registrar o planejamento da Sprint 1`, fora da Sprint 1, como na Etapa 4, e o branch `docs/AB<id>-planejamento-sprint-1`. Nesse branch, salve o molde do Apêndice A em `docs/moldes/task-pronta-para-agente.md`, para que o agente também possa consultá-lo, e comece o `docs/sprint-1-planejamento.md` com as seções listadas em 7.2. O pull request será aberto na Etapa 12.

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
- Nesta etapa, o título e a estimativa bastam. A descrição completa vem na Etapa 11.

A equipe pode criar as Tasks à mão ou pedir ao agente, pela conexão `ado-planejamento`, que crie **exatamente** as Tasks decididas. Confira o resultado no board.

> **Checkpoint 10** — Toda história selecionada tem `[ESP]`, `[BE]`, `[VER]` e `[REV]`, e também `[FE]` quando tem tela. Todas as Tasks têm `Remaining Work` e nenhuma passa de 8h.

---

### Etapa 11 — Detalhar com o agente e auditar (45 min)

1. Com a conexão `ado-planejamento`, peça ao agente a proposta de descrição de cada Task `[BE]` e `[FE]`, seguindo o molde (prompt P1, Apêndice E). **O agente apenas propõe no chat; ninguém altera o work item ainda.** A seção Contrato fica marcada como "a definir na `[ESP]`": ela é preenchida na execução, antes do `[BE]` e do `[FE]` (Etapa 13.2).
2. Audite cada proposta com o checklist do Apêndice B. Para cada sugestão do agente, decida se ela é **aceita**, **modificada** ou **rejeitada**, e registre a decisão e o motivo em `docs/sprint-1-registro-ia.md`, no branch do planejamento.
3. Só depois da auditoria, grave a descrição aprovada na Task, à mão ou pedindo ao agente que grave **o texto aprovado, sem mudanças**.
4. Peça ao agente uma crítica do plano completo (prompt P2). Ele deve apontar:
   - tarefas horizontais;
   - tarefas sem verificação;
   - tarefas grandes demais;
   - risco de violar fronteiras entre módulos;
   - cenários que nenhuma tarefa cobre.

   Registre as decisões da mesma forma.

> **Por que auditar, e não só aceitar.** O agente não conhece a disponibilidade da equipe nem as decisões ainda não registradas, e tende a propor tarefas por camada ("criar entidade", "criar controller"). A auditoria é o momento em que a equipe exerce o julgamento que esta atividade pretende desenvolver.

> **Checkpoint 11** — Todas as Tasks `[BE]` e `[FE]` passam no checklist B, com exceção do contrato, que ainda depende da `[ESP]`. O registro de IA tem uma linha para cada sugestão avaliada, com a decisão e o motivo.

---

### Etapa 12 — Confrontar com a capacidade, registrar riscos e o Definition of Done (25 min)

**12.1 Capacidade.**

1. Em **Boards › Sprints › Taskboard**, abra **Work details** e compare a soma das horas com a capacidade registrada na Etapa 7.
2. Se ultrapassar, **devolva ao backlog a história de menor prioridade** e recalcule.
3. Não reduza números para o plano caber: isso falseia o plano em vez de ajustá-lo.

**12.2 Riscos.** Liste de três a cinco riscos concretos e a resposta prevista para cada um. Pelo menos um deve envolver o agente: cota esgotada, falhas repetidas em uma tarefa ou instabilidade da ferramenta. Se toda a equipe depender de um único caminho de IA, inclua isso entre os riscos.

**12.3 Definition of Done da história.** Ponto de partida obrigatório; a equipe pode acrescentar itens, não retirar.

- [ ] Cada cenário Gherkin coberto por `[BE]` tem um teste de aceitação automatizado com nome correspondente
- [ ] Os checks do pull request mostram o vermelho (commit dos testes) e o verde (commit da implementação)
- [ ] A sabotagem controlada está registrada no pull request, com pelo menos um teste falhando
- [ ] Os cenários foram executados manualmente na aplicação por quem não supervisionou a implementação (`[VER]`)
- [ ] Os pull requests foram revisados por outro integrante com o checklist D, e o CI está verde (testes e fronteiras)
- [ ] Todos os commits e pull requests citam `AB#<id>`
- [ ] As decisões sobre propostas do agente estão no registro de IA
- [ ] Todas as Tasks estão em `Closed`; a história foi movida para `Resolved` por quem executou e para `Closed` pelo guardião da qualidade

**12.4 Encerrar o planejamento.**

1. Complete o `docs/sprint-1-planejamento.md` e abra o pull request do branch do planejamento, com `AB#<id>` da Task da Etapa 10. Integre-o depois da revisão e do CI verde, e feche a Task.
2. Pare o servidor `ado-planejamento` (Caminho 1). No Caminho 2, que não tem modo somente leitura, siga a orientação do Apêndice G. A partir daqui, o agente só **lê** o board.

> **Checkpoint 12** — Nenhuma barra de capacidade ultrapassa o limite. O planejamento, o molde e o registro de IA estão no `main`. A conexão com permissão de escrita está desativada.

---

### Etapa 13 — Executar as tarefas (semanas 1 e 2)

#### 13.1 Antes de começar qualquer Task

1. Atribua a Task a quem vai supervisioná-la e mova-a para `Active`.
2. Para `[BE]` e `[FE]`, confira que a `[ESP]` da história está fechada e que a seção Contrato da Task está preenchida.
3. Para Tasks que geram código (`[BE]`, `[FE]` e correções de Bug), crie um branch a partir do `main` atualizado, no formato `feat/AB<id>-descricao-curta`.
4. Inicie uma **sessão nova** do agente.

#### 13.2 Tarefa `[ESP]` — especificar o contrato

1. Com o apoio do agente, defina para a fatia:
   - a operação (verbo HTTP e rota);
   - os dados de entrada e de saída;
   - as respostas de erro.
2. Indique **qual cenário Gherkin cada resposta cobre**. Um cenário sem resposta correspondente indica contrato incompleto.
3. Grave o contrato, **no navegador**, na seção **Contrato** das Tasks `[BE]` e `[FE]` da história. A `[ESP]` não gera código nem pull request.
4. Feche a `[ESP]`.

#### 13.3 Tarefa `[BE]` — testes primeiro, depois a implementação

1. **Plano.** Peça ao agente que leia a Task e apresente o plano antes de tocar em qualquer arquivo (prompt P3). Confira o plano contra a Task: os arquivos estão dentro do escopo permitido? Há um teste por cenário? Aprove ou corrija.
2. **Testes primeiro.** Peça somente os testes de aceitação, no nível da API (prompt P4).
   - Rode o `<comando-de-verificacao>`. Os testes devem falhar **por asserção**: a funcionalidade ainda não existe.
   - Erro de compilação não conta como vermelho. Se isso acontecer, peça ao agente apenas o mínimo para compilar, sem nenhuma regra de negócio.
   - Faça o commit `test: cenarios de <historia> AB#<id>` e o push.
   - Abra o pull request como **rascunho** (*draft*) para que o CI rode e registre o vermelho.
   - **Espere o check terminar, com falha, antes do próximo push.** Um push novo no mesmo branch cancela a execução em andamento, e o vermelho deixa de ficar registrado.
3. **Implementação.** Peça a implementação mínima para os testes passarem, sem alterar os testes (prompt P5).
   - Rode o `<comando-de-verificacao>`.
   - Faça o commit `feat: <resultado> AB#<id>` e o push. O CI deve ficar verde.
4. **Sabotagem controlada.** Peça ao agente que introduza, sem commit, um único defeito na regra de negócio — nunca nos testes (prompt P6).
   - Rode os testes. **Pelo menos um deve falhar.** Registre qual.
   - Desfaça a alteração e confirme com `git status` que não sobrou nada.
   - Se nenhum teste falhar, os testes não verificam a regra: volte ao passo 2.
5. **Registro de IA.** Acrescente ao `docs/sprint-1-registro-ia.md`, no próprio branch, as decisões sobre as propostas do agente nesta Task.
6. **Pull request.** Preencha o modelo e marque o pull request como pronto para revisão. O modelo deve conter:

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

#### 13.4 Tarefa `[FE]` — tela da fatia

O ciclo é o mesmo: plano, implementação, registro de IA e pull request. A diferença está na verificação:

- a tela deve permitir executar os cenários da história contra a API já integrada;
- a tela deve ser operável **só pelo teclado**;
- o pull request traz uma captura da tela em cada estado relevante: sucesso, erro e vazio.

Testes automatizados de componente são bem-vindos, mas não obrigatórios nesta sprint.

#### 13.5 Tarefas `[VER]` e `[REV]` — verificar e revisar

**`[VER]` — execução manual dos cenários.** Um integrante que não supervisionou a implementação:

1. sobe a aplicação com o comando do `README`;
2. executa cada cenário Gherkin passo a passo;
3. registra o resultado em um comentário da história, nesta forma:

| Cenário | Resultado | Observação |
|---|---|---|

Se algum cenário falhar, crie, no navegador, um work item do tipo `Bug` vinculado à história. A história não fecha com bug aberto.

**`[REV]` — revisão por evidências.** O revisor:

1. aplica o checklist D;
2. pede ao agente que explique o diff (prompt P7);
3. escreve no pull request, **com as próprias palavras**, o que a mudança faz;
4. aprova ou pede mudanças;
5. integra só com a aprovação registrada e o CI verde.

Depois do merge, **uma pessoa** — nunca o agente — fecha as Tasks e zera o `Remaining Work`.

#### 13.6 Ponto de controle no meio da sprint (fim da semana 1, 15 min)

Mantenha o `Remaining Work` atualizado ao longo da sprint; sem isso, o gráfico não significa nada.

1. Abra o **burndown** da sprint (**Boards › Sprints › Analytics**) — o gráfico do trabalho restante ao longo dos dias — e compare-o com a linha ideal.
2. Se a equipe estiver claramente atrasada, decida **agora** qual história de menor prioridade volta ao backlog, para proteger a meta.
3. Registre a decisão em um comentário da história devolvida; ela entra também nas alterações de escopo do encerramento (Etapa 14).

#### 13.7 Protocolo de falha do agente

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

4. Corrija **a Task**, não o código. Registre a causa e a mudança em um comentário do work item, no navegador, e no registro de IA.
5. Recomece em uma sessão nova.
6. Se mais três tentativas falharem, registre um impedimento e leve-o ao docente ou à monitoria.

> **Nunca "resolva" uma falha removendo a verificação.** Desativar um teste, apagar uma verificação de fronteira ou editar o CI para passar transforma a evidência em mentira e invalida o trabalho da Task.

> **Checkpoint 13** — Todo pull request integrado tem as evidências do modelo, revisão registrada e CI verde. O board reflete o trabalho real: nenhuma Task fechada sem pull request integrado e nenhuma Task concluída ainda em `Active`.

---

### Etapa 14 — Verificar a meta e encerrar (30 min, último dia da sprint)

1. **Demonstração.** Mostre a meta funcionando para alguém de fora da equipe (docente, monitoria ou outra equipe), seguindo os cenários das histórias concluídas.
2. **Situação de cada história.** Ou está em `Closed`, com o Definition of Done completo, ou **volta ao backlog**. Não existe "90% pronta".
3. **Encerramento.** Registre em `docs/sprint-1-encerramento.md`, por pull request:
   - a meta foi atingida? Sim, parcialmente ou não, com a evidência;
   - histórias concluídas e devolvidas ao backlog;
   - Tasks planejadas × concluídas;
   - alterações de escopo durante a sprint;
   - falhas do agente por causa (A a E);
   - três lições para a Sprint 2, sendo pelo menos uma sobre especificação.

> **Checkpoint 14** — Alguém de fora da equipe viu a meta funcionar ou entendeu, pela demonstração, por que ela não foi atingida. O board e o encerramento contam a mesma história.

---

## 7. Entregáveis da Parte 2

### 7.1 No Azure Boards

- `Sprint 1` com datas, dias úteis e capacidade de **todos** os integrantes, com ausências marcadas
- Entre 2 e 4 histórias na `Sprint 1`, nenhuma do território de identidade
- Tasks de cada história no molde da Etapa 10, com descrição aprovada na auditoria e `Remaining Work` preenchido
- Commits e pull requests vinculados às Tasks (seção **Development** de cada work item)
- Estados coerentes com o trabalho: histórias em `Closed` ou devolvidas ao backlog ao final da sprint

### 7.2 No repositório `<repositorio-da-equipe>`

- **Código integrado no `main`**, exclusivamente por pull requests aprovados e com CI verde
- **Pull requests** com o modelo da Etapa 13.3 preenchido
- **`docs/sprint-1-planejamento.md`** com as seções:
  1. Meta da sprint
  2. Conta da capacidade, com as horas e o caminho de IA de cada integrante
  3. Justificativa da seleção, incluindo as histórias puladas e o motivo
  4. Esqueleto de tarefas de cada história
  5. Riscos e resposta prevista
  6. Definition of Done
  7. Registro da reunião de planejamento (data, duração e participantes)
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

- **`docs/sprint-1-encerramento.md`**, conforme a Etapa 14
- **`docs/moldes/task-pronta-para-agente.md`**, cópia do Apêndice A, que pode ser adaptada pela equipe

### 7.3 Submissão no Microsoft Teams

Um único post da equipe, contendo:

- link do **Taskboard** da `Sprint 1`;
- link de `<repositorio-da-equipe>`;
- links dos três arquivos de `docs/` desta sprint;
- captura de tela do **burndown** no último dia da sprint;
- nome completo de todos os integrantes.

### 7.4 Checklist da Parte 2

- [ ] Checkpoints 6 a 14 verificados pela equipe
- [ ] `Sprint 1` com datas, dias úteis, capacidade, histórias e Tasks no molde
- [ ] Nenhuma história do território de identidade na sprint
- [ ] Todo código no `main` entrou por pull request aprovado e com CI verde
- [ ] Todo pull request de `[BE]` tem a tabela cenário → teste, o vermelho → verde e a sabotagem
- [ ] Todo commit e pull request cita `AB#<id>`, sem `Fixes`
- [ ] Os três arquivos de `docs/` desta sprint estão no `main`
- [ ] O post no Teams contém todos os links e a captura do burndown

---

## 8. Erros frequentes

| Erro | Consequência | Correção |
|---|---|---|
| Organização do Azure DevOps criada com conta pessoal | O agente não consegue se conectar ao Azure Boards pelo servidor remoto | Usar a organização criada com a conta institucional, ligada ao Microsoft Entra ID |
| Integrantes da organização do GitHub com permissão de leitura | Ninguém além do Owner consegue criar branches | Base permission **Write** (Etapa 1) |
| Pedir ao agente "implemente a história inteira" | Pull request enorme, impossível de revisar; cota consumida de uma vez | Uma Task por sessão, no tamanho do molde |
| Especificar só no chat do agente | O trabalho desaparece com a sessão; ninguém mais consegue continuar | A especificação vive na Task; o chat é descartável |
| Aprovar o plano do agente sem conferir contra a Task | Arquivos fora do módulo e escopo extra | Conferir os arquivos permitidos e os cenários antes de aprovar |
| Implementar antes dos testes | Sem evidência de vermelho; o teste pode estar só confirmando o código | Primeiro commit do branch somente com os testes |
| Enviar a implementação antes de o CI dos testes terminar | O vermelho é cancelado e não fica registrado | Esperar o check vermelho terminar antes do próximo push |
| Aceitar erro de compilação como vermelho | Não prova que o teste verifica o comportamento | O vermelho precisa ser uma falha de asserção |
| Deixar o agente alterar os testes para passar | O teste deixa de verificar o cenário | Rejeitar; testes só mudam com justificativa registrada |
| Desativar teste ou verificação de fronteira para o CI passar | Evidência falsa | Nunca; aplicar o protocolo de falha |
| Insistir com o agente sem limite | Cota e tempo perdidos | Três tentativas; depois, corrigir a especificação |
| Revisar lendo o código "por cima" e aprovar | A revisão vira carimbo | Checklist D e explicação do diff com as próprias palavras |
| Usar `Fixes AB#<id>` | Work item fechado automaticamente, sem Definition of Done | Usar apenas `AB#<id>`; estados são movidos por pessoas |
| Manter a conexão com escrita ativa durante a execução | O agente altera o board | Somente `ado-leitura` a partir da Etapa 13 |
| Registrar a capacidade bruta na aba *Capacity* | As barras não acusam um plano acima do alvo | Registrar as horas por dia do alvo (Etapa 7) |
| Sprint só de back-end | Nada demonstrável a um usuário | Pelo menos uma fatia vertical completa |
| Incluir história de identidade | Fora do escopo desta sprint | Pular e registrar na justificativa da seleção |
| Colar dados pessoais reais em prompts ou dados de teste | Exposição de dados (LGPD) | Usar apenas dados fictícios |

---

## 9. Material de apoio

- **Exemplo de referência — Sprint 1 do PedeJá com agente** (`Exemplo_Referencia_Sprint1_PedeJa.md`): forma e nível esperados, em outro domínio
- Roteiro da **Atividade de Requisitos — Construção do Product Backlog** e o exemplo de backlog do PedeJá
- Apresentação **Arquiteturas de Software** e o ADR-001 da equipe
- `README` do template da solução escolhida
- Material da aula de testes de software
- Documentação oficial:
  - Azure Boards e GitHub: <https://learn.microsoft.com/azure/devops/boards/github/>
  - Servidor MCP remoto do Azure DevOps: <https://learn.microsoft.com/azure/devops/mcp-server/remote-mcp-server>
  - Servidor MCP local do Azure DevOps: <https://github.com/microsoft/azure-devops-mcp/blob/main/docs/GETTINGSTARTED.md>
  - MCP no Codex: <https://developers.openai.com/codex/mcp>
  - Criar uma organização no GitHub: <https://docs.github.com/organizations/collaborating-with-groups-in-organizations/creating-a-new-organization-from-scratch>
  - Criar um repositório a partir de um template: <https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template>

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
- [ ] O contrato está preenchido (`[BE]` e `[FE]`; conferido antes da execução, depois da `[ESP]`)
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
- [ ] **Registro de IA.** As decisões desta Task estão no `docs/sprint-1-registro-ia.md` do próprio pull request
- [ ] **Compreensão.** O revisor escreveu, com as próprias palavras, o que a mudança faz
- [ ] **Dados.** Nenhum segredo, token ou dado pessoal real no código, nos testes ou nos prompts
- [ ] **Front-end** (quando houver). Capturas dos estados de sucesso, erro e vazio; operação pelo teclado verificada

---

## Apêndice E — Prompts de referência

Adapte as palavras, mas mantenha a intenção. Substitua `<id>` pelo número real do work item.

**P1 — Detalhar uma Task** (conexão `ado-planejamento`, Etapa 11)
> Leia a User Story AB#<id> e a Task AB#<id> do projeto Connexa. Seguindo o molde em `docs/moldes/task-pronta-para-agente.md` e as regras do `AGENTS.md`, proponha o texto da descrição desta Task. Deixe a seção Contrato como "a definir na [ESP]". **Não altere nenhum work item**: apenas mostre a proposta e aponte qualquer ambiguidade nos cenários.

**P2 — Criticar o plano** (conexão `ado-planejamento`, Etapa 11)
> Leia todas as Tasks da Sprint 1 do projeto Connexa e as histórias a que pertencem. Avalie o plano contra o molde e o `AGENTS.md` e aponte: tarefas organizadas por camada técnica, tarefas sem forma de verificação, tarefas grandes demais, risco de violar fronteiras entre módulos e cenários que nenhuma tarefa cobre. **Não altere nada.**

**P3 — Planejar a execução** (conexão `ado-leitura`, Etapa 13)
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

**Requisitos:** GitHub Copilot ativo na conta GitHub do integrante (plano Copilot Student ou gratuito); VS Code com a extensão GitHub Copilot Chat; conta institucional com acesso ao projeto `Connexa`, em organização ligada ao Microsoft Entra ID.

1. Confira que o `.vscode/mcp.json` do repositório já tem o nome da organização (Etapa 4). O conteúdo esperado é:

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

2. Inicie o servidor `ado-leitura`, pela visão de servidores MCP do VS Code ou pelo botão **Start** exibido no próprio arquivo.
3. Quando solicitado, autentique-se com a **conta institucional**.
4. Abra o Copilot Chat no modo **Agent** e confira, no seletor de ferramentas, que as ferramentas do Azure DevOps aparecem.
5. Faça o teste: *"Liste os projetos da minha organização no Azure DevOps."*
6. Nas Etapas 10 e 11, inicie também o `ado-planejamento`. Pare-o ao concluir a Etapa 12.

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
   - **Pelo projeto:** o `.codex/config.toml` do repositório já tem o nome da organização (Etapa 4). Marque o projeto como confiável quando o Codex perguntar; a configuração de projeto só vale para projetos confiáveis.
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
- fora das Etapas 10 e 11, **recuse** qualquer chamada que crie ou altere work items.

**Problemas comuns**

| Sintoma | O que fazer |
|---|---|
| No Windows, o servidor não inicia | Troque para `command = "cmd"` e `args = ["/c", "npx", "-y", "@azure-devops/mcp", "<organizacao-azure-devops>", "-d", "core", "work", "work-items"]` |
| `npx` não é reconhecido | Instale o Node.js 20 ou superior e reabra o VS Code |
| O navegador não abre para o login (por exemplo, no Codespaces) | Use o Codex no VS Code da sua máquina, com o repositório clonado localmente |
| O Codex informa limite de uso atingido | O plano gratuito tem cota em janelas de tempo; outro integrante assume a Task ou use o Caminho 1 |
| Erro do *sandbox* do Codex na máquina do laboratório | Comunique o docente; máquinas sem permissão de administrador podem exigir outro modo de execução |

**Privacidade.** Não cole dados pessoais reais em prompts e revise os controles de dados da sua conta ChatGPT.

---

*Roteiro de atividade — Disciplina de Engenharia de Software — Projeto Connexa.*
