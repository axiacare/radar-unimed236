# Integração com Manus AI

Guia técnico para integração do sistema RADAR com o Manus AI.

---

## Visão Geral

O Manus AI é responsável por:

1. **Extrair** dados do Notion via MCP
2. **Processar** e estruturar em JSON
3. **Gerar** Canvas View HTML
4. **Publicar** no GitHub Pages

---

## Skill: radar-export

### Localização

```
/home/ubuntu/skills/radar-export/
├── SKILL.md
├── scripts/
│   └── generate_canvas.py
└── templates/
    └── canvas_template.html
```

### Uso

Para exportar um RADAR, solicite ao Manus:

> "Exporte o RADAR da Semana 05 do Escritório de Valor para Canvas View"

O Manus irá:

1. Buscar a página no Notion
2. Extrair as propriedades
3. Gerar o HTML
4. Fazer commit no repositório
5. O GitHub Actions fará o deploy

---

## Configuração Multi-Tenant

O sistema suporta múltiplos clientes. Cada cliente tem um repositório dedicado:

| Cliente | Código | Repositório | Domínio |
|:---|:---|:---|:---|
| Unimed GV | 236 | axiacare/radar-unimed236 | radar-unimed236.axcare.com.br |

### Arquivo de Configuração

`data/config.json`:

```json
{
  "client_code": "236",
  "client_name": "Unimed Governador Valadares",
  "client_short": "Unimed GV",
  "domain": "radar-unimed236.axcare.com.br",
  "notion": {
    "workspace": "Grupo CSV",
    "database_name": "Central RADAR",
    "database_id": "xxx"
  },
  "branding": {
    "primary_color": "#196396",
    "accent_color": "#2DBF7F",
    "logo_url": "https://files.manuscdn.com/..."
  },
  "teams": [
    "Escritório de Valor",
    "Diretoria Técnica",
    "Superintendência"
  ]
}
```

---

## Fluxo de Exportação

### 1. Buscar Dados

```python
# Via MCP
manus-mcp-cli tool call notion-fetch --server notion --input '{"page_id": "xxx"}'
```

### 2. Estruturar JSON

```json
{
  "data_avaliacao": "02/02/2025",
  "equipe": "Escritório de Valor",
  "avaliador": "Dr. Guilherme Thomé",
  "periodicidade": "Semanal",
  "relatos": ["...", "...", "..."],
  "registros": ["...", "...", "..."],
  "abertos": ["...", "...", "..."],
  "acoes": ["...", "...", "..."],
  "direcionadores": ["...", "...", "..."],
  "definicoes": ["...", "...", "..."],
  "agendas": ["...", "...", "..."],
  "alinhamentos": ["...", "...", "..."],
  "reflexoes": ["...", "...", "..."],
  "recomendacoes": ["...", "...", "..."]
}
```

### 3. Gerar HTML

```bash
python3 /home/ubuntu/skills/radar-export/scripts/generate_canvas.py data.json output.html
```

### 4. Commit e Push

```bash
cd /home/ubuntu/radar-unimed236
cp output.html public/index.html
git add .
git commit -m "RADAR Semana 05 - Escritório de Valor"
git push origin main
```

### 5. Deploy Automático

O GitHub Actions detecta o push e publica no GitHub Pages.

---

## Comandos Úteis

### Listar RADARs recentes

```bash
manus-mcp-cli tool call notion-search --server notion --input '{"query": "RADAR Semana"}'
```

### Buscar página específica

```bash
manus-mcp-cli tool call notion-fetch --server notion --input '{"page_id": "xxx"}'
```

### Gerar Canvas View

```bash
python3 /home/ubuntu/skills/radar-export/scripts/generate_canvas.py input.json output.html
```

---

## Troubleshooting

### Erro: Página não encontrada

Verifique se o ID da página está correto e se o Manus tem acesso ao workspace.

### Erro: Propriedades vazias

A página pode não ter sido processada pela IA do Notion. Clique em "Update" nas propriedades de IA.

### Erro: Deploy falhou

Verifique os logs do GitHub Actions em: `https://github.com/axiacare/radar-unimed236/actions`

---

© 2025 Grupo CSV | AxiaCare. Todos os direitos reservados.
