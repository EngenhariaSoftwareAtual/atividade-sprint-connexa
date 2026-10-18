# Exemplo de referência — Sprint 1 do **PedeJá** com agente de IA

**Disciplina de Engenharia de Software** · Prof. Claudio Nunes
**Finalidade:** material de consulta para a Atividade de Sprint.

> **Por que um domínio diferente do Connexa.** Este exemplo existe para mostrar *forma*, *nível* e *grau de detalhe*, não conteúdo aproveitável. Copiar trechos daqui para o Connexa não funciona: o domínio é outro e as histórias são outras. Use-o para responder "como se faz isso?", nunca "o que devo escrever?".
>
> **Por que não há código de framework.** De propósito. Nesta atividade, o que importa é a especificação, a evidência e a decisão — e é isso que o exemplo mostra.

---

## 1. Ponto de partida

O backlog do PedeJá está no **Exemplo de referência — Backlog do PedeJá**, usado na Atividade de Requisitos. A equipe tem cinco integrantes, cada um com 6 horas por semana para o projeto.

O back-end segue a solução de arquitetura escolhida pela equipe: um monolito modular com os módulos `cardapio`, `pedidos` e `entrega`. A autenticação está fora da Sprint 1, e o template simula um cliente autenticado.

**Parte 1 — preparação do ambiente**, como ficou registrada no post da equipe:

| Item | Registro |
|---|---|
| Organização no GitHub | `pedeja-turma-noite`, com os cinco integrantes, dois deles Owners, e base permission **Write** |
| Repositório | `pedeja-app`, público, criado a partir do template Java |
| Pull request de preparação | #1, vinculado à Task AB#100: ADR-001 (monolito modular em Java) e nome da organização em `.vscode/mcp.json` e `.codex/config.toml`; aprovado por Bruno, CI verde |
| Proteção do `main` | Pull request com 1 aprovação, checks do CI obrigatórios, sem exceções |

| Integrante | Caminho de IA | Teste de fumaça |
|---|---|---|
| Ana, Bruno, Carla | Caminho 1 — GitHub Copilot com o servidor MCP remoto | ok |
| Davi, Elisa | Caminho 2 — Codex com o servidor MCP local | ok, depois de trocar `npx` por `cmd /c npx` no Windows de Elisa |

No PedeJá, o comando único de verificação definido pelo template é `./verificar`.

---

## 2. Meta, capacidade e seleção

**Meta**

> Ao final desta sprint, um cliente consegue ver o cardápio do dia e montar seu pedido no carrinho.

**Capacidade (esforço humano)**

```
Horas por integrante, por semana ................  6h
Integrantes .....................................   5
Semanas .........................................   2
                                              ------
Capacidade bruta ................................  60h
( - ) reserva de 20% ............................  12h
( - ) reuniões da equipe ........................   4h
                                              ------
Capacidade de planejamento ......................  44h
Alvo da primeira sprint (75%) ...................  33h
```

**Escopo selecionado**

| História | Pontos | Esforço humano das Tasks |
|---|---:|---:|
| US-01 — Ver o cardápio disponível hoje (AB#101) | 3 | 9h |
| US-03 — Adicionar um item ao carrinho (AB#103) | 3 | 15h |
| **Total** | **6** | **24h** |

**A folga de 9h não foi preenchida.** A equipe avaliou a US-07 (Informar endereço de entrega, cerca de 8h). Ela caberia na capacidade, mas não sustenta a meta: endereço só importa para enviar o pedido, que está fora desta sprint. Como é a primeira sprint com o fluxo do agente, a folga ficou como reserva. A decisão está na justificativa da seleção.

**Registro na ferramenta.** Na aba *Capacity*, cada integrante ficou com 0,6 h por dia: 33h ÷ 5 integrantes ÷ 10 dias úteis, arredondado para baixo. Assim, as barras de *Work details* comparam o plano com o alvo, e não com a capacidade bruta.

**Onde fica o esforço.** Com o agente, a implementação consome menos horas das pessoas. O esforço de especificar, verificar e revisar **não** diminui — e, como mostra o encerramento, foi maior do que o previsto.

---

## 3. Esqueleto de tarefas

**US-03 — Adicionar um item ao carrinho**

| Task | Executa | Esforço humano |
|---|---|---:|
| AB#110 `[ESP]` Especificar o contrato de inclusão de item no carrinho | Ana | 2h |
| AB#111 `[BE]` Incluir item no carrinho com agrupamento, disponibilidade e limite | Agente, supervisionado por Bruno | 5h |
| AB#112 `[FE]` Botão "adicionar" no cardápio e resumo do carrinho | Agente, supervisionado por Carla | 4h |
| AB#113 `[VER]` Executar os cenários da US-03 na aplicação | Davi | 2h |
| AB#114 `[REV]` Revisar os pull requests da US-03 | Ana | 2h |
| **Total** | | **15h** |

**US-01 — Ver o cardápio disponível hoje**

| Task | Executa | Esforço humano |
|---|---|---:|
| AB#115 `[ESP]` Especificar o contrato da consulta do cardápio do dia | Elisa | 1h |
| AB#116 `[BE]` Listar os itens disponíveis hoje | Agente, supervisionado por Davi | 3h |
| AB#117 `[FE]` Tela do cardápio do dia | Agente, supervisionado por Elisa | 3h |
| AB#118 `[VER]` Executar os cenários da US-01 na aplicação | Carla | 1h |
| AB#119 `[REV]` Revisar os pull requests da US-01 | Bruno | 1h |
| **Total** | | **9h** |

Repare: não há Task "criar o banco de dados" nem "criar o controller". Toda Task entrega comportamento que pode ser verificado. Quem executa `[VER]` e `[REV]` nunca é quem supervisionou a implementação.

---

## 4. A Task `[BE]` da US-03, pronta para agente

Este é o texto gravado no work item AB#111 **depois** da auditoria (seção 5) e da `[ESP]`.

```markdown
Título: [BE] Incluir item no carrinho com agrupamento, disponibilidade e limite — US-03

## Objetivo
O cliente atual consegue incluir um item do cardápio no carrinho, e a resposta
traz as linhas e o total atualizados.

## História e cenários
História: AB#103 (US-03 — Adicionar um item ao carrinho)
Cenários cobertos por esta Task:
  "item disponível adicionado ao carrinho vazio"
  "mesmo item adicionado duas vezes"
  "item indisponível"
  "item inexistente"
  "limite de itens por pedido"
Cenários fora desta Task: nenhum. As mensagens exibidas ao cliente são
responsabilidade da [FE] AB#112.

## Contrato  (definido na [ESP] AB#110)
Operação: POST /api/pedidos/carrinho/itens
Entrada: itemId (texto, obrigatório). Cada inclusão acrescenta 1 unidade.
Saída (200): linhas [{ itemId, nome, quantidade, subtotal }], totalUnidades, total
Erros:
  422 ITEM_INDISPONIVEL   quando o item está indisponível hoje → "item indisponível"
  404 ITEM_NAO_ENCONTRADO quando o item não existe no cardápio → "item inexistente"
  422 LIMITE_DE_ITENS     quando o carrinho já tem 20 unidades → "limite de itens por pedido"
Em todos os erros, o carrinho permanece inalterado.

## Escopo
Pode alterar: módulo pedidos, pasta pedidos/carrinho/
Pode usar sem alterar: CardapioApi.itemDisponivelHoje(itemId), API pública do módulo cardapio
Não pode alterar: testes existentes, CI, configuração de fronteiras,
                  dependências do projeto, módulos cardapio e entrega

## Verificação
Comando: ./verificar
Pronto quando: os testes de aceitação dos cinco cenários acima passam
e nenhuma verificação existente falha.

## Fora de escopo
Remover item e alterar quantidade (US-04 e US-05); cupom (US-06); qualquer tela.
```

---

## 5. A auditoria — trecho do registro de IA

| # | Work item | Proposta do agente | Decisão | Motivo |
|---|---|---|---|---|
| D1 | AB#111 | Dividir a Task em "criar entidade Carrinho", "criar repositório" e "criar endpoint" | Rejeitada | Tarefas por camada; nenhuma delas entrega comportamento verificável sozinha |
| D2 | AB#111 | Verificar a disponibilidade lendo diretamente a tabela de itens do cardápio | Modificada | Cada módulo é dono dos seus dados; usar `CardapioApi.itemDisponivelHoje` |
| D3 | AB#103 | Apontou ambiguidade: "20 itens" são linhas do carrinho ou unidades? | Aceita | A equipe decidiu: unidades, a soma das quantidades. O cenário foi reescrito e a decisão, comentada na história |
| D4 | AB#111 | Responder 404 para item inexistente | Aceita | Comportamento real que a história não cobria; o cenário "item inexistente" foi acrescentado à US-03 antes da execução |
| D5 | AB#111 | Criar `CarrinhoUtils` no módulo `comum` "para reuso futuro" | Rejeitada | `comum` não tem regra de negócio, e não há segundo uso hoje |
| D6 | Plano (P2) | Nenhuma Task cobre as mensagens exibidas ao cliente nos cenários de erro | Aceita | Critério acrescentado à `[FE]` AB#112 |
| D7 | AB#111 | Acrescentar um cenário para quantidade negativa | Rejeitada nesta sprint | A inclusão é sempre de 1 unidade; alterar a quantidade é a US-05. Registrado para o refinamento |

**Efeito da decisão D3 no critério de aceite da US-03**

```gherkin
# Antes
Dado que o carrinho contém 20 itens, o máximo permitido por pedido

# Depois
Dado que o carrinho contém 20 unidades no total, o máximo permitido por pedido
```

**Cenário acrescentado pela decisão D4**

```gherkin
Cenário: item inexistente
  Dado que não existe item com o código "X99" no cardápio de hoje
  Quando o cliente tenta adicionar "X99" ao carrinho
  Então o item não é adicionado
    E a mensagem informa que o item não foi encontrado
```

---

## 6. Execução da `[BE]` — o pull request

### Um teste que passou cedo demais

No commit dos testes, o esperado eram cinco testes vermelhos. Vieram **quatro**. O teste do cenário "item inexistente" passou antes de existir qualquer implementação.

Bruno, que supervisionava, investigou. A rota ainda não existia, então a aplicação respondia 404 para qualquer chamada — e o teste conferia **apenas** o código 404. Ele pediu ao agente que o teste também verificasse o código de erro `ITEM_NAO_ENCONTRADO` no corpo da resposta. Com isso, os cinco testes ficaram vermelhos pelo motivo certo.

> Um teste que passa antes da implementação não está verificando o que diz verificar.

### O pull request #14, como foi aberto para revisão

```markdown
## Work items
AB#111 · AB#103

## O que muda
O módulo pedidos passa a aceitar a inclusão de um item no carrinho do cliente atual.
Antes de mexer no carrinho, consulta o cardápio pela API pública: se o item não existe
ou está indisponível, devolve erro e o carrinho fica como estava. Itens repetidos viram
uma linha só, com a quantidade somada. Acima de 20 unidades, a inclusão é recusada.

## Cenário → teste
| Cenário (Gherkin)                              | Teste                                            |
|------------------------------------------------|--------------------------------------------------|
| item disponível adicionado ao carrinho vazio   | adiciona_item_disponivel_em_carrinho_vazio       |
| mesmo item adicionado duas vezes               | agrupa_item_repetido_em_uma_linha                |
| item indisponível                              | recusa_item_indisponivel_sem_alterar_carrinho    |
| item inexistente                               | recusa_item_inexistente_sem_alterar_carrinho     |
| limite de itens por pedido                     | recusa_inclusao_acima_de_20_unidades             |

## Vermelho → verde
- 3f9c2a1 test: cenarios de US-03 AB#111 — 4 falharam, 1 passou (investigado, ver c41e7d8)
- c41e7d8 test: verifica codigo de erro do item inexistente AB#111 — 5 falharam por asserção
- 8b71d05 feat: inclusao de item no carrinho AB#111 — check verde

## Sabotagem controlada
- Defeito 1: limite verificado como "maior que 21" em vez de "maior que 20"
  → falhou recusa_inclusao_acima_de_20_unidades
- Defeito 2: agrupamento de itens repetidos desligado
  → falhou agrupa_item_repetido_em_uma_linha
- Alterações desfeitas; git status limpo

## Decisões sobre propostas do agente
D1, D2, D4 e D5 em docs/sprint-1-registro-ia.md
```

### A revisão (`[REV]` AB#114, por Ana)

> **Checklist D.** Escopo ok: só `pedidos/carrinho/` e testes novos; nada em CI, fronteiras ou dependências. Rastreabilidade ok: o vínculo aparece em AB#111 e AB#103. Cenário → teste: 5 de 5. Vermelho → verde e sabotagem registrados. CI verde, incluindo as fronteiras.
>
> **Com as minhas palavras:** a inclusão pergunta ao módulo de cardápio se o item existe e está disponível. Se não, devolve o erro e não toca no carrinho. Se o carrinho já tem 20 unidades, recusa. Senão, soma 1 à linha do item ou cria uma linha nova.
>
> **Pedido de mudança:** `recusa_item_indisponivel_sem_alterar_carrinho` só confere o código 422. O nome promete que o carrinho fica inalterado, mas nada verifica isso — é o caso do teste que verifica só parte do resultado (Apêndice C). Peça ao agente a asserção do estado do carrinho depois da recusa.

Depois do ajuste e de um novo check verde, Ana aprovou e integrou. Bruno fechou a Task AB#111 e zerou o `Remaining Work`.

---

## 7. Uma falha do agente — a `[FE]` da US-01

Para "simplificar", a equipe havia apagado da Task AB#117 a linha *"Não pode alterar: dependências do projeto"*, por achar que ela não se aplicava a uma tela.

| Tentativa | O que aconteceu |
|---|---|
| 1 | O agente adicionou uma biblioteca de componentes visuais ao projeto; o build falhou por conflito de versões |
| 2 | Para corrigir, o agente alterou a configuração do build — fora do escopo; Elisa rejeitou |
| 3 | O agente removeu a biblioteca, mas a lista de itens não podia ser operada pelo teclado |

Depois da terceira tentativa, Elisa parou, descartou o branch e classificou a falha:

- **Causa:** A — especificação incompleta. A Task não proibia mudar as dependências e não dizia que a tela devia ser operável pelo teclado.
- **Mudança na Task:** a linha das dependências voltou para "Não pode alterar", e a condição "operável só pelo teclado" entrou em "Verificação".

Em uma sessão nova, o agente concluiu a Task na primeira tentativa.

> A falha não estava no agente: estava na Task. Cada linha do molde existe por um motivo.

---

## 8. Verificação manual — comentário de Davi na US-03 (`[VER]` AB#113)

| Cenário | Resultado | Observação |
|---|---|---|
| item disponível adicionado ao carrinho vazio | ok | |
| mesmo item adicionado duas vezes | ok | Uma linha, quantidade 2, total R$ 48,00 |
| item indisponível | ok | Mensagem exibida junto ao item |
| item inexistente | não executável pela tela | A tela só oferece itens existentes; coberto pelo teste automatizado |
| limite de itens por pedido | **falhou** | A tela exibiu o texto técnico do erro da API, não a mensagem do cenário → Bug AB#120 |

O Bug AB#120 foi vinculado à US-03 e corrigido no pull request #19, revisado por Ana. Davi repetiu o cenário e marcou ok. Só então a US-03 foi para `Resolved` e, depois, para `Closed` pelo guardião da qualidade.

Os testes automatizados verificavam a API, e a API estava certa. Foi a execução manual que encontrou o problema na experiência do cliente.

---

## 9. Encerramento — trecho de `docs/sprint-1-encerramento.md`

- **Meta:** atingida. Demonstrada à monitoria no último dia, seguindo os cenários da US-01 e da US-03.
- **Histórias:** US-01 e US-03 em `Closed`. Nenhuma devolvida ao backlog.
- **Tasks:** 10 planejadas e 10 concluídas, mais 1 bug criado e resolvido (AB#120).
- **Esforço humano:** 24h planejadas e 27h registradas. A verificação levou mais tempo do que o previsto.
- **Falhas do agente:** 1, com causa A (AB#117).
- **Lições para a Sprint 2:**
  1. Não editar o molde para "simplificar": cada linha existe por um motivo.
  2. Reservar mais tempo para `[VER]`: os cenários de erro na tela levaram o dobro do previsto.
  3. Ao conferir o vermelho, olhar também os testes que **passaram** antes da implementação.

---

## 10. O que este exemplo pretende ensinar

| Ponto | Onde aparece |
|---|---|
| O primeiro pull request já testa a cadeia work item → commit → pull request | Seção 1 |
| Com agente, o esforço cai na implementação, mas não na verificação | Seções 2 e 9 |
| Folga de capacidade não justifica item que não sustenta a meta | Seção 2 |
| Tarefas por fatia vertical, nunca por camada | Seção 3 e decisão D1 |
| A auditoria muda o plano — e às vezes a própria história | Decisões D3 e D4 |
| Fronteiras de módulo escritas na especificação | Seção 4 (Escopo) e decisões D2 e D5 |
| Teste que passa antes da implementação é suspeito | Seção 6 |
| Teste cujo nome promete mais do que a asserção verifica | Seção 6, revisão |
| A sabotagem prova que o teste verifica a regra | Seção 6 |
| Falha do agente costuma ser defeito da Task | Seção 7 |
| A verificação manual encontra o que os testes não cobrem | Seção 8 |

---

*Material de apoio — Disciplina de Engenharia de Software — Projeto Connexa.*
