# RADAR | Unimed Governador Valadares (236)

> **Revisão Ágil de Demandas, Ações e Reflexões**

Sistema de gestão de reuniões e acompanhamento estratégico para a Unimed Governador Valadares (código ANS: 236), operado pela AxiaCare como parte do ecossistema Grupo CSV.

---

## Visão Geral

Este repositório contém a infraestrutura de documentação e visualização do método RADAR aplicado às operações da Unimed GV e Unihealth GV. O sistema integra-se com o Notion para captura de dados e gera Canvas Views de alta definição para apresentações e relatórios.

### Stack Tecnológico

| Componente | Tecnologia | Função |
|:---|:---|:---|
| **Armazenamento** | Notion Database | Captura e estruturação de dados |
| **Processamento** | Manus AI + Python | Extração e transformação |
| **Visualização** | HTML/CSS estático | Canvas View de alta definição |
| **Hospedagem** | GitHub Pages | Publicação automática |
| **DNS** | Cloudflare | Domínio customizado |
| **CI/CD** | GitHub Actions | Deploy automatizado |

---

## Estrutura do Repositório

```
radar-unimed236/
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions para deploy automático
├── docs/
│   ├── metodologia/
│   │   └── RADAR.md            # Documentação completa do método
│   ├── notion/
│   │   └── INTEGRACAO.md       # Guia de integração com Notion
│   └── integracao/
│       └── MANUS.md            # Integração com Manus AI
├── public/
│   ├── index.html              # Canvas View principal
│   ├── css/
│   │   └── styles.css          # Estilos do Canvas View
│   ├── js/
│   │   └── main.js             # Scripts (se necessário)
│   └── assets/
│       └── logos/              # Logos e imagens
├── data/
│   └── config.json             # Configuração do cliente
├── templates/
│   └── canvas_template.html    # Template base para geração
└── README.md                   # Este arquivo
```

---

## Cliente

### Unimed Governador Valadares

| Campo | Valor |
|:---|:---|
| **Código ANS** | 236 |
| **Nome Fantasia** | Unimed Governador Valadares |
| **Razão Social** | Unimed Governador Valadares Cooperativa de Trabalho Médico |
| **UF** | MG |
| **Cidade** | Governador Valadares |
| **Domínio RADAR** | radar-unimed236.axcare.com.br |

### Unihealth GV

Hospital gerido pelo ICDS (Instituto de Ciências da Saúde) vinculado à operadora.

---

## Metodologia RADAR

O RADAR é uma metodologia proprietária desenvolvida pelo Dr. Guilherme Thomé para gestão de reuniões estratégicas em saúde.

### Acrônimo

| Letra | Significado | Descrição |
|:---|:---|:---|
| **R** | Relatos / Registros | Informações relevantes e documentação |
| **A** | Abertos / Ações | Pendências identificadas e ações definidas |
| **D** | Direcionadores / Definições | Prioridades estratégicas e decisões |
| **A** | Agenda / Alinhamentos | Compromissos e alinhamentos necessários |
| **R** | Reflexões / Recomendações | Análises críticas e sugestões |

### Fluxo de Trabalho

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Reunião       │────▶│   Notion        │────▶│   Manus AI      │
│   (Gravação)    │     │   (Estruturação)│     │   (Processamento)│
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                                        │
                                                        ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Stakeholders  │◀────│   GitHub Pages  │◀────│   Canvas View   │
│   (Visualização)│     │   (Publicação)  │     │   (HTML)        │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

---

## Integração com Notion

### Base de Dados: Central RADAR

A Central RADAR no Notion contém todas as páginas de reunião estruturadas com as seguintes propriedades:

| Propriedade | Tipo | Descrição |
|:---|:---|:---|
| `Semana` | Date | Data da semana de referência |
| `Time` | Select | Equipe responsável |
| `Resumo da IA` | Text (AI) | Estruturação automática do conteúdo |
| `RADAR_Consolidado` | Text (AI) | Versão final consolidada |
| `Relato_01` a `Relato_03` | Text | Relatos relevantes |
| `Registro_01` a `Registro_03` | Text | Registros documentados |
| `Aberto_01` a `Aberto_03` | Text | Pendências abertas |
| `Ação_01` a `Ação_03` | Text | Ações definidas |
| ... | ... | (30 propriedades no total) |

### Data Lake RADAR

Página de referência com dicionário de termos, nomes e siglas para correção automática de transcrições.

---

## Integração com Manus AI

### Skill: radar-export

A skill `radar-export` no Manus é responsável por:

1. **Buscar dados** da página RADAR no Notion via MCP
2. **Estruturar** os dados em formato JSON
3. **Gerar** o Canvas View HTML
4. **Fazer commit** no repositório GitHub
5. **Disparar** o deploy automático via GitHub Actions

### Configuração Multi-Tenant

O sistema suporta múltiplos clientes através do arquivo `data/config.json`:

```json
{
  "client_code": "236",
  "client_name": "Unimed Governador Valadares",
  "domain": "radar-unimed236.axcare.com.br",
  "notion_database_id": "xxx",
  "branding": {
    "primary_color": "#196396",
    "accent_color": "#2DBF7F",
    "logo_url": "https://..."
  }
}
```

---

## Deploy

### GitHub Actions

O deploy é automatizado via GitHub Actions. A cada push na branch `main`, o workflow:

1. Faz checkout do código
2. Copia arquivos para a pasta de publicação
3. Publica no GitHub Pages

### Domínio Customizado

- **URL**: https://radar-unimed236.axcare.com.br
- **DNS**: CNAME apontando para `axiacare.github.io`
- **SSL**: Gerenciado pelo GitHub Pages

---

## Branding

### Cores

| Token | Hex | Uso |
|:---|:---|:---|
| `csv-blue` | `#196396` | Cor primária |
| `csv-green` | `#2DBF7F` | Acento |
| `csv-dark` | `#1b1e24` | Textos |
| `csv-light` | `#f4f6f8` | Fundos |

### Tipografia

- **Primária**: Inter (Google Fonts)
- **Pesos**: 400, 500, 600, 700, 800

### Logos

- AxiaCare horizontal positivo
- Grupo CSV (rodapé)

---

## Licença

Proprietário. © 2025 Grupo CSV | AxiaCare. Todos os direitos reservados.

---

## Contato

- **AxiaCare**: [axcare.com.br](https://axcare.com.br)
- **Grupo CSV**: [grupocsv.com](https://grupocsv.com)
- **Email**: contato@grupocsv.com
