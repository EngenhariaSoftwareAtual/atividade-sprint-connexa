# Sprint 1 — Projeto Connexa

Material didático da disciplina de **Engenharia de Software** para a primeira sprint do projeto **Connexa**, realizada em equipes de 4 a 5 alunos.

Na Sprint 1, a equipe planeja a sprint no **Azure Boards** e materializa as tarefas em código com um **agente de IA no VS Code** (GitHub Copilot ou Codex), que lê os work items diretamente do Azure Boards por meio de um servidor **MCP**. O código é escrito pelo agente; a equipe especifica, verifica, revisa e decide o que entra no produto.

> O objetivo da atividade é ensinar **práticas de engenharia** — planejamento por capacidade, decomposição, especificação, verificação, revisão, rastreabilidade e integração —, e não a construção de código em um framework específico.

## Objetivos de aprendizagem

Ao concluir a atividade, a equipe deverá ser capaz de:

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
| Product Backlog construído e corrigido | Atividade **RA-01 — Construção do Product Backlog** |
| Noções de teste de software: níveis de teste, vermelho → verde, checklist de teste ruim, sabotagem controlada | Aula de testes de software |
| Organização GitHub da equipe e repositório `connexa-equipe-NN` criado a partir do scaffold da stack escolhida, com ADR-001 e CI verde | Roteiro do scaffold |

## Sequência da atividade

Siga o [roteiro da Sprint 1](RA-02_Roteiro_Sprint1_Planejamento_e_Execucao.md). Em resumo:

| Etapa | Conteúdo |
|---|---|
| 0 | Conectar o Azure Boards ao GitHub e o agente ao Azure Boards; teste de fumaça |
| 1 a 4 | Configurar a sprint, calcular a capacidade de esforço humano, escrever a meta e selecionar de 2 a 4 histórias |
| 5 e 6 | Montar o esqueleto de tarefas e detalhá-lo com o agente, com auditoria registrada |
| 7 | Confrontar com a capacidade, registrar riscos e o Definition of Done |
| 8 | Executar as tarefas: testes primeiro, implementação, sabotagem, pull request e revisão por evidências |
| 9 | Verificar a meta e registrar o encerramento |

**Principais entregas**

- Sprint 1 configurada no Azure Boards, com Tasks no molde e vínculos com os pull requests
- Código integrado no `main` somente por pull requests aprovados e com CI verde
- `docs/sprint-1-planejamento.md`, `docs/sprint-1-registro-ia.md` e `docs/sprint-1-encerramento.md` no repositório da equipe

## Organização dos arquivos

| Arquivo | Finalidade |
|---|---|
| `RA-02_Roteiro_Sprint1_Planejamento_e_Execucao.md` | Roteiro da atividade, com rubrica, checklists, prompts de referência e instruções de conexão (Apêndices A a G) |
| `Exemplo_Referencia_Sprint1_PedeJa.md` | Exemplo completo em outro domínio: Task pronta para agente, auditoria, pull request revisado, falha do agente e encerramento |

O exemplo usa o domínio do PedeJá e mostra a forma e o nível esperados. Ele **não** deve ser copiado para o Connexa.

## Ferramentas

- **Gestão do trabalho:** Azure Boards, processo Agile, com contas institucionais
- **Código e revisão:** GitHub, na organização criada pela equipe, com repositório público
- **Agente de IA:** VS Code com GitHub Copilot (servidor MCP remoto do Azure DevOps) ou Codex (servidor MCP local)
- **Submissão:** Microsoft Teams, conforme a seção de entregáveis do roteiro

Leia o roteiro integralmente antes de iniciar. Os checkpoints de cada etapa devem ser verificados pela equipe antes da submissão.

---

**Disciplina de Engenharia de Software** · Prof. Claudio Nunes
