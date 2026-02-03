# Integração com Notion

Guia técnico para integração do sistema RADAR com o Notion.

---

## Visão Geral

O Notion serve como a camada de armazenamento e estruturação de dados do RADAR. Todas as reuniões são registradas em uma base de dados centralizada chamada **Central RADAR**.

---

## Base de Dados: Central RADAR

### Localização

- **Workspace**: Grupo CSV
- **Caminho**: Central de Equipes > Central RADAR
- **ID do Database**: `[configurado em data/config.json]`

### Propriedades

#### Metadados

| Propriedade | Tipo | Descrição |
|:---|:---|:---|
| `ID` | Number | Identificador único |
| `Semana` | Date | Data da semana de referência |
| `Time` | Select | Equipe responsável |
| `Periodicidade` | Select | Frequência (Semanal, Quinzenal, etc.) |
| `Localizador` | Formula | Identificador calculado |

#### Propriedades de IA

| Propriedade | Tipo | Descrição |
|:---|:---|:---|
| `Resumo da IA` | Text (AI Autofill) | Estruturação automática do conteúdo |
| `RADAR_Consolidado` | Text (AI Autofill) | Versão final consolidada |
| `AI_content` | Text (AI Autofill) | Conteúdo auxiliar |

#### Propriedades de Conteúdo (30 campos)

**Relatos / Registros**
- `Relato_01`, `Relato_02`, `Relato_03`
- `Registro_01`, `Registro_02`, `Registro_03`

**Abertos / Ações**
- `Aberto_01`, `Aberto_02`, `Aberto_03`
- `Ação_01`, `Ação_02`, `Ação_03`

**Direcionadores / Definições**
- `Direcionador_01`, `Direcionador_02`, `Direcionador_03`
- `Definição_01`, `Definição_02`, `Definição_03`

**Agenda / Alinhamentos**
- `Agenda_01`, `Agenda_02`, `Agenda_03`
- `Alinhamento_01`, `Alinhamento_02`, `Alinhamento_03`

**Reflexões / Recomendações**
- `Reflexão_01`, `Reflexão_02`, `Reflexão_03`
- `Recomendação_01`, `Recomendação_02`, `Recomendação_03`

---

## Template de Página

O template padrão **RADAR | {Semana}** inclui:

1. **Cabeçalho** com propriedades visíveis
2. **Corpo** para transcrição/anotações
3. **Seção Resumo da IA** para estruturação automática
4. **Seção RADAR_Consolidado** para versão final

---

## Prompts de IA

### Resumo da IA

```
Leia o conteúdo do corpo desta página e a página "Data Lake RADAR" para referência de nomes e termos.

Estruture o conteúdo no formato RADAR, usando marcadores explícitos:

**Relatos / Registros**
- **Relato 01:** [Conteúdo]
- **Registro 01:** [Conteúdo]
...

**Abertos / Ações**
- **Aberto 01:** [Conteúdo]
- **Ação 01:** [Conteúdo]
...

[continua para todas as seções]

IMPORTANTE: Corrija a grafia de nomes próprios conforme o Data Lake RADAR.
```

### RADAR_Consolidado

```
Leia a propriedade "Resumo da IA" e as 30 propriedades individuais.

Regras:
1. Se a propriedade individual estiver preenchida, use-a (prioridade manual).
2. Se estiver vazia, use o valor do "Resumo da IA".
3. Se ambas estiverem vazias, deixe vazio.

Gere a saída no formato visual estruturado.
```

---

## Data Lake RADAR

Página de referência contendo:

- **Pessoas**: Nomes e cargos
- **Instituições**: Nomes oficiais
- **Projetos**: Nomenclaturas padronizadas
- **Siglas**: Definições

Esta página é consultada pela IA para correção automática de transcrições.

---

## Acesso via MCP

O Manus acessa o Notion via MCP (Model Context Protocol):

```bash
# Buscar página
manus-mcp-cli tool call notion-fetch --server notion --input '{"page_id": "xxx"}'

# Pesquisar
manus-mcp-cli tool call notion-search --server notion --input '{"query": "RADAR Semana 05"}'
```

---

## Fluxo de Dados

```
Transcrição/Anotações
        │
        ▼
   Corpo da Página
        │
        ▼
   Resumo da IA (automático)
        │
        ▼
   Propriedades Manuais (opcional)
        │
        ▼
   RADAR_Consolidado (automático)
        │
        ▼
   Manus (extração via MCP)
        │
        ▼
   Canvas View HTML
        │
        ▼
   GitHub Pages (publicação)
```

---

© 2025 Grupo CSV | AxiaCare. Todos os direitos reservados.
