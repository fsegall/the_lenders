# ⚖️ Módulo `foundry/` — Contrato Inteligente de Empréstimo

Este módulo conterá o contrato inteligente responsável por formalizar e executar os empréstimos da plataforma entre-chain-lend. Utiliza o framework [Foundry](https://book.getfoundry.sh/) para desenvolvimento, teste e deploy em redes EVM.

---

## 🎯 Objetivo

- Registrar pedidos de empréstimo validados por prova ZK
- Permitir financiamento peer-to-peer com controle de saldo
- Controlar reembolso, prazo e eventuais juros
- Verificar se o usuário possui `passed = 1` via input público

---

## ⚙️ Stack

- [Foundry](https://book.getfoundry.sh/)
- Solidity >= 0.8.x
- Testnet Ethereum (Sepolia, Goerli, etc)
- Viem (no frontend) para interação
- zk-credit para validação prévia

---

## 📁 Estrutura Recomendada

```
foundry/
├── src/
│   └── LoanContract.sol         # Contrato principal
├── script/
│   └── DeployLoan.s.sol         # Script de deploy
├── test/
│   └── LoanContract.t.sol       # Testes com Forge
├── foundry.toml
└── README.md
```

---

## 🔒 Regras de Negócio Esperadas

- O contrato recebe uma função `createLoanRequest(...)`
  - Exige `passed == true` como input público (verificado via frontend)
- A função `fundLoan(...)` registra o financiamento por outro endereço
- A função `repayLoan(...)` permite reembolso com ou sem juros
- Pode incluir lógica de reputação, penalidade, e registro histórico

---

## 🧪 Testes

- Use `forge test` para testar os fluxos:
  - Criação de pedido
  - Financiamento
  - Reembolso
  - Tentativas inválidas

---

## 🚀 Deploy

Utilize Foundry para deploy em testnet:

```bash
forge script script/DeployLoan.s.sol --rpc-url $SEPOLIA_RPC --private-key $KEY --broadcast --verify
```

---

## 🔗 Integração com Frontend

- O frontend usa Viem para ler e escrever no contrato
- A lógica de `passed = 1` deve ser verificada **antes** do contrato ser chamado
- O contrato confia apenas em entradas públicas (sem prova ZK direta)

---

## 💡 Extensões futuras

- Verificar `proof` diretamente no contrato (via verifier on-chain)
- Suporte a múltiplos financiadores por pedido
- Cálculo de score on-chain como fallback (caso ZK falhe)

---

> Desenvolvido como parte do MVP entre-chain-lend por Felipe Segall
