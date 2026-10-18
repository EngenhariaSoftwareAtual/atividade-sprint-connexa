# Atividade de Sprint — Projeto Connexa

Material didático da disciplina de **Engenharia de Software** para a primeira sprint do projeto **Connexa**, realizada em equipes de 4 a 5 alunos.

Na Sprint 1, a equipe prepara o próprio repositório a partir do template da solução de arquitetura escolhida, planeja a sprint no **Azure Boards** e materializa as tarefas em código com um **agente de IA no VS Code** (GitHub Copilot ou Codex), que lê os work items diretamente do Azure Boards por meio de um servidor **MCP**. O código é escrito pelo agente; a equipe especifica, verifica, revisa e decide o que entra no produto.

> O objetivo da atividade é ensinar **práticas de engenharia** — planejamento por capacidade, decomposição, especificação, verificação, revisão, rastreabilidade e integração —, e não a construção de código em um framework específico.

## Objetivos de aprendizagem

Ao concluir a atividade, a equipe deverá ser capaz de:

- preparar um repositório a partir de um template e conectá-lo ao Azure Boards e ao agente;
- planejar uma sprint a partir da meta e da capacidade real da equipe;
- decompor histórias em tarefas verticais, prontas para serem executadas por um agente;
- escrever especificações que um agente consiga executar, com escopo e verificação explícitos;
- exigir e conferir testes de aceitação antes da implementação (vermelho → verde e sabotagem controlada);
- revisar pull requests a partir de evidências;
- manter a rastreabilidade do work item até o código integrado;
- registrar e justificar as decisões tomadas sobre as propostas do agente.

## Pré-requisitos

| Pré-requisito | Onde |
|---|---|
| Product Backlog construído e corrigido, no projeto `Connexa` de uma organização do Azure DevOps criada com a conta institucional (Microsoft Entra ID) | [Atividade de Requisitos — Construção do Product Backlog](https://github.com/EngenhariaSoftwareAtual/atividade-requisitos-connexa) |
| Noções de teste de software: níveis de teste, vermelho → verde, checklist de teste ruim, sabotagem controlada | Aula de testes de software |
| Solução de arquitetura escolhida pela equipe | Apresentação Arquiteturas de Software |

## Sequência da atividade

Siga o [roteiro da Sprint 1](Roteiro_Sprint1_Planejamento_e_Execucao.md). A atividade tem duas partes, cada uma com a sua entrega.

### Parte 1 — Preparação do ambiente (Aula 1)

| Etapa | Conteúdo |
|---|---|
| 1 | Criar a organização da equipe no GitHub |
| 2 | Criar o repositório a partir do template da solução escolhida (`connexa-modelo-java`, `connexa-modelo-dotnet` ou `connexa-modelo-node`) |
| 3 | Conectar o Azure Boards ao repositório |
| 4 | Preparar o repositório, registrar o ADR-001 e proteger o `main`, com o primeiro pull request vinculado a um work item |
| 5 | Conectar o agente ao Azure Boards e fazer o teste de fumaça |

**Entrega da Parte 1:** organização e repositório criados, ADR-001 no `main` por pull request vinculado, `main` protegido e agente de cada integrante lendo o board.

### Parte 2 — Planejamento, execução e encerramento (Aula 2 e as duas semanas da sprint)

| Etapa | Conteúdo |
|---|---|
| 6 e 7 | Configurar a sprint e os dias úteis; calcular e registrar a capacidade de esforço humano |
| 8 e 9 | Escrever a meta e selecionar de 2 a 4 histórias |
| 10 e 11 | Montar o esqueleto de tarefas e detalhá-lo com o agente, com auditoria registrada |
| 12 | Confrontar com a capacidade, registrar riscos e o Definition of Done |
| 13 | Executar as tarefas: testes primeiro, implementação, sabotagem, pull request e revisão por evidências |
| 14 | Verificar a meta e registrar o encerramento |

**Entrega da Parte 2:** Sprint 1 no Azure Boards com Tasks no molde e vínculos com os pull requests; código integrado no `main` somente por pull requests aprovados e com CI verde; `docs/sprint-1-planejamento.md`, `docs/sprint-1-registro-ia.md` e `docs/sprint-1-encerramento.md` no repositório da equipe.

## Organização dos arquivos

| Arquivo | Finalidade |
|---|---|
| `Roteiro_Sprint1_Planejamento_e_Execucao.md` | Roteiro da atividade, com checklists, prompts de referência e instruções de conexão (Apêndices A a G) |
| `Exemplo_Referencia_Sprint1_PedeJa.md` | Exemplo completo em outro domínio: preparação, Task pronta para agente, auditoria, pull request revisado, falha do agente e encerramento |

O exemplo usa o domínio do PedeJá e mostra a forma e o nível esperados. Ele **não** deve ser copiado para o Connexa.

## Ferramentas

- **Gestão do trabalho:** Azure Boards, processo Agile, com contas institucionais
- **Código e revisão:** GitHub, na organização criada pela equipe, com repositório público criado a partir do template
- **Agente de IA:** VS Code com GitHub Copilot (servidor MCP remoto do Azure DevOps) ou Codex (servidor MCP local)
- **Submissão:** Microsoft Teams, uma entrega ao fim de cada parte

Leia o roteiro integralmente antes de iniciar. Os checkpoints de cada etapa devem ser verificados pela equipe antes de cada submissão.

---

**Disciplina de Engenharia de Software** · Prof. Claudio Nunes
