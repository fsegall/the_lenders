# 🛠️ Roadmap de Desenvolvimento — entre-chain-lend

## 🧩 Epics

- **Identidade e Autenticação Web3**
- **Cadastro e Perfil de Usuário**
- **Análise de Crédito com Agente ZK**
- **Geração e Verificação de Provas ZK**
- **Financiamento P2P com Smart Contracts**
- **Dashboard do Usuário**
- **UI/UX da Plataforma**
- **Documentação Técnica e Pitch**

---

## 🚩 Milestones e Issues --> [`Kanban Interativo`](kanban-roadmap-interativo.html)

### ✅ M1: Setup e Integrações Iniciais
- [x] Setup do projeto base (React + Viem) — _`setup`, `frontend`_
- [x] Conectar carteira Web3 ao frontend — _`web3`, `frontend`_
- [x] Criar layout inicial (landing + navegação) — _`ui/ux`_

### ✅ M2: Autenticação e Cadastro
- [x] Implementar login Web3 (Supabase + wallet-auth) — _`supabase`, `auth`_
- [x] Criar e persistir perfil (empreendedor/financiador) — _`perfil`, `backend`_
- [x] Criar formulário de lances de empréstimo — _`frontend`, `formulário`_
- [x] Listar lances públicos — _`frontend`, `listagem`_

### ✅ M3: Análise de Crédito com ZK
- [x] Criar estratégia de automação de score com N8N — _`credit-agent`, `score`_
- [ ] Criar fluxo automatizado de score com N8N — _`credit-agent`, `score`_
- [x] Gerar prova ZK local com Circom/snarkjs — _`zk-credit`, `prova`_
- [x] Verificar prova via ZKVerify com Edge Function — _`supabase`, `verificação`_

### ✅ M4: Smart Contracts e Reembolso
- [ ] Criar smart contract de empréstimo (Foundry) — _`foundry`, `contrato`_
- [ ] Testar contrato com Forge — _`foundry`, `testes`_
- [ ] Implementar lógica de reembolso — _`solidity`, `contrato`_
- [ ] Integrar contrato ao frontend (Viem) — _`web3`, `integração`_

### ✅ M5: Dashboard, Polimento e UI
- [ ] Exibir status dos pedidos (aceito, financiado, quitado) — _`frontend`, `dashboard`_
- [x] UI para ações como “financiar” e “quitar” — _`ui/ux`, `ações`_
- [x] Responsividade e refino visual — _`ui/ux`, `ajustes`_

### ✅ M6: Entregas Finais
- [x] Criar documentação técnica por módulo — _`documentação`, `README`_
- [x] Gerar diagramas ER e arquitetura — _`diagramas`, `visual`_
- [x] Preparar pitch técnico (PDF + script) — _`pitch`, `apresentação`_
- [ ] Gravar vídeo de apresentação do MVP — _`pitch`, `vídeo`_
