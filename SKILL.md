# TODO Guide — Template de Auditoria de Qualidade

Use este skill sempre que o usuário pedir para criar, atualizar ou revisar o `TODO.md` de auditoria de qualidade do projeto.

---

## Estrutura do TODO.md

O arquivo `TODO.md` deste projeto segue um formato fixo. Respeite rigorosamente esta estrutura.

### Cabeçalho (comentado — não renderizado)

```markdown
<!-- # Refatoração — Backlog de Qualidade

| ID | Nível | Descrição | Arquivo | Skills | Status |
|:--:|:-----:|:----------|:--------|:-------|:------:|

--- -->
```

> Este bloco existe por compatibilidade com um backlog tabular anterior. Mantenha-o comentado, não o remova.

---

### Seção de Auditoria

```markdown
# Auditoria de Qualidade — React & TypeScript

> Gerado em YYYY-MM-DD. Apenas arquivos de produção (não-teste) auditados.
> Categorias: **[REACT]** padrões React · **[TS]** TypeScript · **[QUALITY]** qualidade geral · **[DEPRECATED]** recurso sem uso/órfão
> Severidades: 🔴 HIGH · 🟡 MEDIUM · 🟢 LOW

---
```

Atualize a data sempre que gerar uma nova auditoria completa.

---

### Blocos de severidade

Cada severidade tem seu próprio bloco `##`:

```markdown
## 🔴 HIGH — Crítico (resolver com prioridade)

## 🟡 MEDIUM — Importante (resolver em breve)

## 🟢 LOW — Melhoria (resolver quando conveniente)
```

---

### Formato de cada item

Cada problema encontrado deve seguir este padrão dentro do bloco de severidade correspondente:

```markdown
### `caminho/relativo/ao/arquivo.ts` — Título curto do problema

- **[CATEGORIA]** Linhas X–Y (se aplicável): descrição objetiva do problema. Explique o risco ou impacto.
- **Ação**: o que deve ser feito para resolver. Uma ou duas frases, direto ao ponto.
```

**Categorias válidas:**

| Tag | Quando usar |
|-----|-------------|
| `[REACT]` | Violações de padrões React: efeitos desnecessários, dependências erradas, cleanup ausente, re-renders evitáveis |
| `[TS]` | Problemas TypeScript: `any`, type assertions sem guard, tipos frouxos, discriminated unions ausentes |
| `[QUALITY]` | Qualidade geral: código duplicado, abstrações desnecessárias, strings hardcoded, inconsistências de estilo |
| `[DEPRECATED]` | Recursos sem consumidores: exports mortos, hooks órfãos, arquivos não importados |

**Regras de severidade:**

| Nível | Critério |
|-------|----------|
| 🔴 HIGH | Risco real em produção: memory leak, loop infinito, crash silencioso, type assertion que mascara erro de runtime, arquivo completamente órfão |
| 🟡 MEDIUM | Dívida técnica relevante: efeito com deps instáveis, estado com combinações inválidas, cast sem guard, código duplicado crítico |
| 🟢 LOW | Melhorias de qualidade: inline handlers, `||` vs `??`, fragmentos desnecessários, nomes inconsistentes, `useMemo` redundante |

---

### Como marcar itens como concluídos

Quando uma tarefa é executada, **não delete o item e não remova o conteúdo original** — mantenha a descrição do problema e adicione uma linha `Resolução:` ao final:

```markdown
### ~~`caminho/arquivo.ts` — Título do problema~~ ✅ CORRIGIDO

- **[CATEGORIA]** Linhas X–Y: descrição original do problema.
- **Ação**: o que estava previsto para resolver.
- **Resolução**: o que foi feito de fato.
```

Para itens deletados (DEPRECATED):

```markdown
### ~~`caminho/arquivo.ts`~~ ✅ DELETADO

- **[DEPRECATED]** Descrição original do problema.
- **Resolução**: motivo da remoção e o que foi excluído.
```

Para itens resolvidos indiretamente (como consequência de outra tarefa):

```markdown
### ~~`caminho/arquivo.ts` — Título~~ ✅ CORRIGIDO (junto com HIGH)

- **[CATEGORIA]** Linhas X–Y: descrição original do problema.
- **Ação**: o que estava previsto.
- **Resolução**: resolvido como consequência de [outra tarefa]; o que foi feito.
```

Quando **todos os itens de um bloco** estiverem concluídos, atualize o título do bloco:

```markdown
## 🔴 HIGH — Crítico ✅ Todas concluídas
```

---

### Exemplo de item pendente vs. concluído

**Pendente:**
```markdown
### `src/hooks/useAuthService.ts` — Double assertion sem guard

- **[TS]** Linha 43: `response.data as unknown as LoginResponse` não tem garantia em runtime.
- **Ação**: criar type-guard `isLoginResponse(v: unknown): v is LoginResponse` e aplicá-lo antes de acessar `access_token`.
```

**Concluído:**
```markdown
### ~~`src/hooks/useAuthService.ts` — Double assertion sem guard~~ ✅ CORRIGIDO

- **[TS]** Linha 43: `response.data as unknown as LoginResponse` não tem garantia em runtime.
- **Ação**: criar type-guard `isLoginResponse(v: unknown): v is LoginResponse` e aplicá-lo antes de acessar `access_token`.
- **Resolução**: adicionado type-guard `isLoginResponse` que valida `access_token` antes de acessar os campos.
```

---

## Manual de Uso — Quando gerar uma auditoria

> **Importante**: o escopo da auditoria (quais pastas, quais tipos de problemas) é sempre definido pelo usuário. Não presuma categorias ou critérios — audite apenas o que foi solicitado.

1. **Leia** todos os arquivos de produção (não-teste) das pastas solicitadas.
2. **Classifique** cada problema em categoria `[REACT]`, `[TS]`, `[QUALITY]` ou `[DEPRECATED]`.
3. **Atribua** severidade (HIGH / MEDIUM / LOW) com base nos critérios da tabela.
4. **Escreva** os itens do mais crítico para o menos crítico dentro de cada bloco.
5. **Inclua sempre** o caminho relativo do arquivo, linhas quando relevante, o impacto do problema e uma ação clara.
6. **Nunca** execute código — apenas documente.

---

## Manual de Atualização — Durante execução de tarefas

Siga estas regras ao trabalhar em tarefas do TODO:

1. **Antes de começar** uma tarefa: anuncie no chat (em português) qual tarefa está sendo feita e o que será alterado.
2. **Ao concluir** uma tarefa: marque o título com `~~strikethrough~~ ✅ CORRIGIDO/DELETADO` e adicione uma linha `Resolução:` **abaixo do conteúdo original** — não substitua o conteúdo.
3. **Nunca delete** o texto original dos itens do TODO — mantenha a descrição do problema e a ação prevista visíveis para code review.
4. **Se uma tarefa resolver itens adicionais** (ex.: corrigir um HIGH também resolve um MEDIUM): marque os extras com `✅ CORRIGIDO (junto com X)` e adicione a linha `Resolução:`.
5. **Quando todos os itens de um bloco** estiverem concluídos: atualize o título do bloco com `✅ Todas concluídas`.
6. **Atualize a data** no cabeçalho da seção de auditoria quando gerar uma nova auditoria completa.

---

## Prompt base para solicitar nova auditoria

Use este prompt quando quiser gerar uma nova auditoria completa:

```
Faça uma auditoria de qualidade nas pastas [lista de pastas], auditando APENAS os arquivos que não são testes.

Documente tudo no TODO.md seguindo o template do skill `todo-guide`. Não execute nenhuma alteração de código — apenas documente.
```
