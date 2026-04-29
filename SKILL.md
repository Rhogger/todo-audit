---
name: todo-audit
description: Estrategista de Backlog e Qualidade para orquestrar o ciclo de vida de tarefas técnicas (P1-P4). Use para auditar o código, identificar débitos técnicos e gerenciar o arquivo TODO.md de forma estruturada e cronológica.
---

## Estrutura do TODO.md

O arquivo `TODO.md` deve seguir uma estrutura limpa, hierárquica por prioridade e organizada cronologicamente.

### Cabeçalho Informativo

```markdown
# Backlog de Desenvolvimento e Qualidade

> Última atualização: YYYY-MM-DD
> Escala de Prioridade: **P1** (Crítico) · **P2** (Importante) · **P3** (Melhoria) · **P4** (Exploração)

---
```

---

## Blocos de Prioridade

As tarefas devem ser agrupadas nos seguintes blocos, do mais urgente para o menos urgente:

### `## 🔴 P1 — Crítico (Impacto Imediato)`
*   **Critério**: Bugs impeditivos (blockers), falhas graves de segurança (SQLi, vazamentos), erros que causam crash ou requisitos obrigatórios para o release imediato.

### `## 🟡 P2 — Importante (Próximos passos)`
*   **Critério**: Funcionalidades core, dívida técnica que atrasa a equipe, problemas de UX significativos ou falta de estabilidade em fluxos principais.

### `## 🟢 P3 — Melhoria (Quando conveniente)`
*   **Critério**: Refatorações para legibilidade, otimizações de performance, melhorias de logs/telemetria ou modernização de libs não críticas.

### `## 🔵 P4 — Exploração / Backlog (Futuro)`
*   **Critério**: Ideias de novas features, prototipagem, experimentos de arquitetura ou tarefas "nice-to-have".

---

## Organização por Data e Tags

Dentro de cada bloco de prioridade, as tarefas são agrupadas pela **data da última manipulação** (criação ou atualização).

### Regra de Cabeçalho de Data:
1. Ao manipular uma tarefa, verifique se existe o cabeçalho `#### YYYY-MM-DD` dentro do bloco de prioridade.
2. Se existir, insira/atualize a tarefa sob ele.
3. Se não existir, crie o cabeçalho `#### YYYY-MM-DD` no **topo** do bloco de prioridade e insira a tarefa.

### Sistema de Tags:
Cada tarefa deve conter tags entre colchetes no início da descrição para facilitar a busca:
- **Intuito**: `[BUG]`, `[FEATURE]`, `[REFACTOR]`, `[HOTFIX]`, `[BUILD]`, `[CICD]`, `[DOCS]`.
- **Tecnologia**: `[TS]`, `[JS]`, `[REACT]`, `[VUE]`, `[RUBY]`, `[JAVA]`, `[DOCKER]`, etc.
- **Exemplo**: `[BUG][REACT][TS]`

---

## Formato de Cada Item

```markdown
### `contexto` — Título curto

#### YYYY-MM-DD
- **Tags**: `[INTUITO][TECNOLOGIA]`
- **Descrição**: O que é o problema ou a necessidade.
- **Ação**: O que deve ser feito.
```

---

## Fluxo de Atualização (Lifecycle)

### 1. Adicionando/Atualizando Tarefas
*   Mantenha a prioridade correta.
*   Siga a regra do **Cabeçalho de Data** (sempre mova ou crie no topo da seção para destacar o que é novo).
*   Garanta que as **Tags** identifiquem claramente o intuito e a stack.

### 2. Marcando como Concluído
Mantenha o histórico formatando o título com tachado e adicionando a resolução sob a data atual:

```markdown
### ~~`contexto` — Título da tarefa~~ ✅ CONCLUÍDO

#### 2026-04-29 (Finalizado)
- **Tags**: `[REFACTOR][TS]`
- **Resolução**: Descrição técnica do que foi feito.
```

---

## Manual de Uso para a IA

1.  **Contextualização**: Sempre identifique o intuito e a tecnologia antes de registrar.
2.  **Cronologia**: Se estiver atualizando uma tarefa antiga, mova-a para o bloco de data de hoje dentro da prioridade dela.
3.  **Busca Otimizada**: Use as tags para agrupar logicamente suas ações quando estiver trabalhando em lote.

---

## Prompt de Exemplo

> "Audite os arquivos de build. Adicione as falhas encontradas ao `TODO.md` como P1, usando tags de [BUILD] e [DOCKER], organizando pela data de hoje."
