# 🤖 Módulo `credit-agent/` — Análise de Crédito Automatizada (N8N)

Este módulo representa o componente de automação responsável por calcular e entregar o `score de crédito` do usuário para a aplicação. Utiliza o [n8n.io](https://n8n.io) como plataforma de orquestração de fluxos de dados e agentes inteligentes.

---

## 🧭 Objetivo

- Calcular um score de crédito a partir de dados externos e internos
- Retornar o resultado para o frontend ou backend
- Ativar a geração da prova ZK com base no score retornado

---

## ⚙️ Stack

- [n8n](https://n8n.io/) — plataforma de automação open-source
- Supabase REST API
- Webhooks HTTP
- (Opcional) APIs externas para consulta de score
- (Futuro) Integração com IA ou ML para cálculo do score

---

## 🔁 Fluxo Geral

```
    A[Usuário cria perfil na plataforma] --> B[Supabase armazena perfil]
    B --> C[N8N detecta novo perfil ou requisição de empréstimo]
    C --> D[Busca dados do usuário (perfil, histórico, etc)]
    D --> E[Calcula score]
    E --> F[Retorna JSON para frontend ou backend]
    F --> G[Geração da prova ZK com zk-credit]
    G --> H[Verificação com ZKVerify via Supabase]
```

---

## 🧱 Estrutura Recomendada

```
credit-agent/
├── flows/
│   └── calculate_credit_score.json     # Export do fluxo N8N
├── docs/
│   └── fluxo-anotado.png               # Fluxograma explicativo
└── README.md
```

---

## 📤 Formato de Saída Esperado

O agente pode retornar um JSON como:

```json
{
  "score": 720,
  "threshold": 650,
  "passed": true
}
```

---

## 🧪 Integração com zk-credit

A saída do agente será usada como `input.json` para gerar a prova ZK localmente:

```json
{
  "score": "720",
  "threshold": "650"
}
```

---

## 🔌 Integração com Supabase

Você pode:
- Usar webhook para acionar o N8N com o `user_id`
- Consultar a tabela `profiles` diretamente via HTTP
- Inserir score calculado em uma tabela `credit_scores` com FK para `profiles`

---

## 🔒 Privacidade e Segurança

- O `score` é tratado como **variável temporária**
- Nunca deve ser salvo em campos públicos
- A única saída pública é `passed = 1` dentro da prova ZK

---

## 🚀 Como testar localmente

1. Inicie o N8N via Docker ou CLI:
   ```bash
   docker run -it --rm      -p 5678:5678      -v ~/.n8n:/home/node/.n8n      n8nio/n8n
   ```

2. Importe o fluxo `calculate_credit_score.json` no editor visual

3. Teste o webhook via Postman ou diretamente do frontend

---

> Desenvolvido como parte do MVP entre-chain-lend por Felipe Segall
