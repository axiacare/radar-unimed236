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

---

## Ecossistema Grupo CSV

O Grupo CSV (Cuidados em Saúde com Valor) é um ecossistema estratégico que integra gestão, educação e tecnologia para entregar valor sustentável em saúde.

### A Tríade

| Braço | Função | Foco | Site |
|:---|:---|:---|:---|
| **AxiaCare®** | Gestão & Estratégia | Consultoria, Governança Clínica, Operação | [axcare.com.br](https://axcare.com.br) |
| **MedValor®** | Educação & Cultura | Formação de Lideranças, Mudança de Mindset | [medvalor.com.br](https://medvalor.com.br) |
| **TheraTech®** | Tecnologia & IA | Desenvolvimento de Software, Inteligência de Dados | [thera.tech](https://thera.tech) |

---

## Estrutura do Repositório

```
radar-unimed236/
├── docs/
│   ├── metodologia/
│   │   └── RADAR.md            # Documentação completa do método
│   ├── notion/
│   │   └── INTEGRACAO.md       # Guia de integração com Notion
│   └── integracao/
│       └── MANUS.md            # Integração com Manus AI
├── public/
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
├── index.html                  # Canvas View principal
├── CNAME                       # Domínio customizado
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

Hospital gerido pelo ICDS (Instituto de Cooperação para o Desenvolvimento da Saúde) vinculado à operadora.

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
5. **Publicar** automaticamente via GitHub Pages

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

### GitHub Pages (Deploy from Branch)

O deploy é realizado automaticamente pelo GitHub Pages a partir da branch `main`. A cada push, o conteúdo da raiz do repositório é publicado no domínio customizado.

**Configuração:**
- **Source**: Deploy from a branch
- **Branch**: main
- **Folder**: / (root)

### Domínio Customizado

- **URL**: https://radar-unimed236.axcare.com.br
- **DNS**: CNAME apontando para `axiacare.github.io`
- **SSL**: Gerenciado pelo Cloudflare/GitHub Pages

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

| Marca | Site | Descrição |
|:---|:---|:---|
| **Grupo CSV** | [grupocsv.com](https://grupocsv.com) | Ecossistema de Valor em Saúde |
| **AxiaCare®** | [axcare.com.br](https://axcare.com.br) | Gestão e Consultoria |
| **MedValor®** | [medvalor.com.br](https://medvalor.com.br) | Conteúdo e Ensino |
| **TheraTech®** | [thera.tech](https://thera.tech) | Tecnologia e Desenvolvimento |

**Email**: contato@grupocsv.com
