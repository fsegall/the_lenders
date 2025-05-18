# ⚙️ n8n - Workflow de Análise de Crédito

Este módulo contém o fluxo automatizado no n8n responsável por calcular o score de crédito de um usuário com base em dados armazenados no Supabase, formatar o resultado e enviá-lo para validação via ZK proof.

---

## 🧠 Visão Geral

```mermaid
graph TD
  A[Webhook de Entrada] --> B[Consulta Supabase (tabela: profiles)]
  B --> C[Cálculo do Score]
  C --> D[Formatação da Resposta]
  D --> E[Webhook de Saída]
  D --> F[Webhook para zk-credit]
```

---

## 📌 Webhook

- **Método**: `GET`
- **Endpoint**: `/webhook/credit-analysis`
- **Exemplo de chamada**:

```bash
curl https://webhook.n8n.alifa.com.br/webhook/credit-analysis
```

---

## 📊 Lógica de Score

O cálculo considera os seguintes fatores:

- `+100` se renda > 5000
- `+50` se tempo de emprego > 2 anos
- `+70` se possui imóvel
- `-80` se possui dívidas
- `-100` por inadimplências
- Limite do score: `300 - 850`
- `threshold = 650` (mínimo para aprovação)

---

## 📤 Saídas

### 1. Webhook normal

```json
{
  "score": 720,
  "threshold": 650,
  "passed": true
}
```

### 2. Formato para zk-credit

```json
{
  "score": "720",
  "threshold": "650"
}
```

---

## 📁 Arquivo do Workflow

Este módulo inclui o arquivo exportado do n8n:

- [`workflow_hackathon.json`](./workflow_hackathon.json)

Você pode importá-lo diretamente em sua instância do n8n.

---

## 🔗 Integração com zk-credit

A saída do webhook `zk-credit` é consumida pelo frontend, que chama a edge function `credit-verify` com os dados recebidos para gerar a ZK proof.

---

## ✅ Status

- [x] Consulta Supabase
- [x] Cálculo seguro do score
- [x] Resposta bifurcada (usuário + zk-credit)
- [x] Totalmente integrado ao MVP