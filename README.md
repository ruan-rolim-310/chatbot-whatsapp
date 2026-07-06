# 🤖 Chatbot WhatsApp com IA

Sistema de atendimento automatizado para WhatsApp utilizando Inteligência Artificial, desenvolvido com NestJS, LangChain, LangGraph e WAHA.

O projeto foi criado para automatizar vendas e atendimento, permitindo que clientes realizem pedidos diretamente pelo WhatsApp enquanto a IA consulta informações de estoque, histórico de conversas e regras de negócio para responder de forma contextualizada.

---

## 🚀 Funcionalidades

- 📱 Integração com WhatsApp via WAHA
- 🤖 Atendimento automatizado com IA
- 🧠 Memória de contexto da conversa
- 👤 Cadastro automático de clientes
- 💬 Histórico de mensagens
- 📦 Controle de estoque
- 🛒 Gestão de pedidos
- 🏪 Regras de negócio personalizadas
- 🔄 Webhook para recebimento de mensagens
- 💾 Persistência utilizando TypeORM

---

## 🏗️ Arquitetura

```text
WhatsApp
    │
    ▼
WAHA
    │
    ▼
Webhook (/waha/webhook)
    │
    ├── Cliente
    ├── Histórico
    ├── Estoque
    ├── Pedidos
    │
    ▼
Prompt Builder
    │
    ▼
LangGraph + LangChain
    │
    ▼
Modelo de IA
    │
    ▼
Resposta
    │
    ▼
WAHA → WhatsApp
```

---

## 🛠️ Tecnologias

### Backend

- NestJS
- TypeScript
- TypeORM
- SQLite

### Inteligência Artificial

- LangChain
- LangGraph
- OpenAI
- Google Generative AI (Gemini)

### Integrações

- WAHA (WhatsApp HTTP API)
- Axios

### Infraestrutura

- Docker
- Docker Compose

---

## 📂 Estrutura do Projeto

```text
src/
├── customer/
│   ├── entities/
│   ├── dto/
│   └── services
│
├── messages/
│   ├── entities/
│   ├── dto/
│   └── services
│
├── stock/
│   ├── entities/
│   ├── dto/
│   └── services
│
├── product/
│   ├── entities/
│   ├── dto/
│   └── services
│
├── order/
│   ├── entities/
│   ├── dto/
│   └── services
│
├── prompt/
│   └── geração de prompts
│
├── waha/
│   └── integração WhatsApp
│
├── work-graph/
│   ├── graphs/
│   ├── tools/
│   └── agentes LangGraph
│
├── database/
└── config/
```

---

## ⚙️ Como Funciona

Quando um cliente envia uma mensagem:

1. O WAHA recebe a mensagem.
2. O webhook é acionado.
3. O sistema verifica se o cliente existe.
4. Caso não exista, cria automaticamente.
5. Busca o histórico da conversa.
6. Consulta os produtos disponíveis em estoque.
7. Monta um prompt contextualizado.
8. Envia para o agente de IA.
9. Salva pergunta e resposta.
10. Retorna a resposta para o WhatsApp.

---

## 📦 Instalação

### Clonar repositório

```bash
git clone https://github.com/ruan-rolim-310/chatbot-whatsapp.git

cd chatbot-whatsapp
```

### Instalar dependências

```bash
npm install
```

---

## 🔧 Variáveis de Ambiente

Crie um arquivo `.env`:

```env
PORT=3000

OPENAI_API_KEY=sua_chave

GOOGLE_API_KEY=sua_chave

WAHA_URL=http://localhost:4000
WAHA_API_KEY=admin
```

> Ajuste as variáveis conforme sua implementação.

---

## ▶️ Executando Localmente

Modo desenvolvimento:

```bash
npm run start:dev
```

Build:

```bash
npm run build
```

Produção:

```bash
npm run start:prod
```

---

## 🐳 Docker

O projeto disponibiliza um ambiente com:

- Redis
- PostgreSQL
- WAHA
- n8n

Subir infraestrutura:

```bash
docker compose up -d
```

Serviços:

| Serviço | Porta |
|----------|---------|
| WAHA | 4000 |
| PostgreSQL | 5432 |
| Redis | 6379 |
| n8n | 5678 |

---

## 📡 Endpoints

### Health Check

```http
GET /waha/health
```

Resposta:

```json
{
  "status": "healthy"
}
```

---

### Webhook WhatsApp

```http
POST /waha/webhook
```

Recebe mensagens enviadas pelo WAHA.

---

## 🧠 Inteligência Artificial

O agente utiliza:

- Histórico do cliente
- Produtos disponíveis
- Quantidades em estoque
- Dados cadastrais
- Regras de negócio
- Contexto da conversa

O sistema gera prompts dinâmicos para garantir respostas coerentes e alinhadas ao fluxo de vendas.

---

## 📊 Entidades Principais

### Cliente

```text
- id
- nome
- telefone
```

### Mensagem

```text
- id
- conteúdo
- timestamp
- cliente
```

### Produto

```text
- id
- nome
- preço
```

### Estoque

```text
- quantidade
- reservado
- validade
- lote
```

### Pedido

```text
- cliente
- itens
- valor total
```

---

## 🔄 Fluxo de Atendimento

```text
Cliente
   ↓
WhatsApp
   ↓
WAHA
   ↓
Webhook
   ↓
Consulta Cliente
   ↓
Consulta Histórico
   ↓
Consulta Estoque
   ↓
Prompt
   ↓
IA
   ↓
Resposta
   ↓
WhatsApp
```

---

## 🧪 Testes

```bash
npm run test
```

Cobertura:

```bash
npm run test:cov
```

Testes E2E:

```bash
npm run test:e2e
```

---

## 📈 Melhorias Futuras

- [ ] Painel administrativo
- [ ] Dashboard de vendas
- [ ] Integração com Pix automática
- [ ] Reconhecimento de áudio
- [ ] Catálogo com imagens
- [ ] Múltiplos atendentes
- [ ] Multiempresa
- [ ] Integração com ERP

---

## 👨‍💻 Autor

Ruan Rolim

GitHub:
https://github.com/ruan-rolim-310

---

## 📄 Licença

Projeto para fins de estudo e desenvolvimento interno.
