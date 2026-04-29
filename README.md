# TODO Audit — Estrategista de Backlog Universal 🚀

Este é um **Agent Skill** projetado para transformar o arquivo `TODO.md` de um projeto em uma ferramenta estratégica de orquestração de desenvolvimento. Ele permite que IAs e desenvolvedores colaborem na manutenção de um backlog técnico organizado, rastreável e priorizado, independente da linguagem ou framework.

## 🎯 Propósito

O objetivo desta skill é eliminar o "caos" dos arquivos de tarefas, implementando um sistema de:

- **Priorização Estratégica (P1-P4):** Do crítico ao exploratório.
- **Rastreabilidade Cronológica:** Organização automática por data de manipulação.
- **Busca Otimizada por Tags:** Identificação instantânea de intuito (`[BUG]`, `[FEATURE]`) e tecnologia (`[REACT]`, `[RUBY]`).
- **Histórico de Resolução:** Registro imutável do que foi feito, mantendo o contexto original.

---

## 🛠️ Detalhamento de Prioridades

As tarefas são classificadas para garantir que o esforço da equipe esteja sempre no lugar certo:

### 🔴 P1 — Crítico (Impacto Imediato)

- **Critério:** Bugs impeditivos (blockers) que impedem o uso do software, falhas graves de segurança (ex: injeção de SQL, vazamento de dados), erros que causam crash em produção ou requisitos obrigatórios para o próximo release imediato.
- **Foco:** Resolução em tempo real.

### 🟡 P2 — Importante (Débito Técnico e Core)

- **Critério:** Funcionalidades principais em desenvolvimento, dívida técnica que impacta a velocidade da equipe, problemas de UX significativos que não impedem o uso mas prejudicam a experiência, ou melhorias de estabilidade necessárias a curto prazo.
- **Foco:** Planejamento para o próximo ciclo/sprint.

### 🟢 P3 — Melhoria (Qualidade e Performance)

- **Critério:** Refatorações não urgentes para melhorar a legibilidade, otimizações de performance (micro-otimizações), ajustes de consistência visual, melhorias em logs e telemetria, ou modernização de bibliotecas não críticas.
- **Foco:** Execução quando houver janelas de manutenção.

### 🔵 P4 — Exploração (Futuro e Insights)

- **Critério:** Ideias para novas funcionalidades, prototipagem de tecnologias, experimentos de arquitetura, atualizações cosméticas ou tarefas do tipo "seria bom ter".
- **Foco:** Documentação para não perder a ideia; baixo compromisso de entrega.

---

## 📝 Como funciona

### 1. Criando uma Nova Tarefa (P1)

Quando a IA identifica um problema crítico, ela organiza assim:

```markdown
## 🔴 P1 — Crítico (Resolver agora)

#### 2026-04-29

### `src/auth/session.ts` — Falha na expiração de token

- **Tags**: `[BUG][TS][HOTFIX]`
- **Descrição**: Tokens expirados não estão sendo invalidados no lado do cliente.
- **Ação**: Implementar interceptor para capturar 401 e limpar o localStorage.
```

### 2. Atualizando e Concluindo uma Tarefa

Ao finalizar, a tarefa é mantida para histórico, mas marcada com tachado:

```markdown
### ~~`src/auth/session.ts` — Falha na expiração de token~~ ✅ CONCLUÍDO

#### 2026-04-30 (Finalizado)

- **Tags**: `[BUG][TS][HOTFIX]`
- **Resolução**: Interceptor adicionado ao Axios; tokens agora são removidos automaticamente no erro 401.
```

---

## 🚀 Como instalar

```bash
npx skills add Rhogger/todo-audit
```

## 🤖 Exemplos de Uso

### Auditoria Profunda

**Prompt**: "Realize uma Auditoria Profunda em todo o projeto. Utilize skills como `codebase_investigator` para mapear a arquitetura e `generalist` para análise detalhada de código. O objetivo é identificar pontos de melhoria em qualidade técnica, eliminando edge cases como race conditions, re-renders desnecessários, falta de type guards e vulnerabilidades latentes. Use a skill `todo-audit` exclusivamente para organizar e registrar essas descobertas no `TODO.md` com as prioridades P1-P4."

### Auditoria de Pasta Específica

**Prompt**: "Realize uma auditoria de qualidade técnica na pasta `[caminho]`. Analise a conformidade com Clean Code, robustez do tratamento de erros, eficiência de algoritmos e integridade da tipagem. Registre todas as melhorias necessárias no `TODO.md` através da skill `todo-audit`."

### Anotação (Demandas e Ideias)

**Prompt**: "Utilize a skill `todo-audit` para anotar a seguinte demanda/ideia que não foi registrada em ferramentas externas (Jira/Trello): `[descrição da tarefa]`. Classifique o impacto e urgência para definir a prioridade (P1-P4) e adicione as tags tecnológicas pertinentes."

### Atualização de Tarefa

**Prompt**: "Concluí a migração do banco. Atualize o TODO.md marcando a tarefa correspondente como concluída e descreva o que foi feito."

---
