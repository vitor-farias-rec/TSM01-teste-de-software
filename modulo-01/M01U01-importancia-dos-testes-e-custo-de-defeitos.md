# Atividade Avaliativa: Análise de Defeitos — Relatório PsicoCare

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 1 |
| **Sistema Analisado** | [PsicoCare](https://github.com/andrelbribeiro/clinica-psi) |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Analisar o cenário fictício do sistema **PsicoCare** fornecido pelo professor, identificando a fase do ciclo de vida ideal para a detecção de cada defeito, os impactos para o usuário e para o negócio, e a correlação com o gráfico do custo de correção de bugs.

---

## Análise Detalhada dos Defeitos

### Defeito 1 – Ficha de Anamnese
* **Fase ideal de detecção:** `Teste de Integração` — Um teste que confirme a gravação real no banco de dados (e não apenas a mensagem visual de sucesso) identificaria a falha antes da fase de teste de sistema.
* **Impacto no usuário:** A recepcionista acredita ter concluído o cadastro, mas na consulta seguinte não haverá ficha registrada, gerando retrabalho e atendimento sem histórico médico.
* **Impacto no negócio:** Perda de dados sensíveis de saúde (protegidos pela LGPD) e risco severo de insatisfação e reclamações dos pacientes.

---

### Defeito 2 – Agenda de Consultas
* **Fase ideal de detecção:** `Teste Unitário` — A regra *"um psicólogo não pode ter dois agendamentos no mesmo horário"* falhou na lógica de verificação de conflito. Um teste unitário isolado com dados simulados valida essa regra sem necessidade do sistema completo rodando.
* **Impacto no usuário:** Conflito de horários no qual o paciente ou o psicólogo chega para a consulta e não consegue ser atendido.
* **Impacto no negócio:** Dano direto à reputação da clínica e sobrecarga operacional do profissional de saúde.

---

### Defeito 3 – Cadastro do Psicólogo
* **Fase ideal de detecção:** `Teste Unitário` — Validação de formato de campo, sendo uma das etapas de teste mais simples e baratas de implementar.
* **Impacto no usuário:** Nenhum impacto imediato na navegação, mas compromete a confiabilidade dos registros do sistema.
* **Impacto no negócio:** Risco de não conformidade (*compliance*) com o Conselho de Psicologia, visto que a clínica precisa garantir que apenas profissionais com CRP válido atuem.

---

### Defeito 4 – Controle Financeiro
* **Fase ideal de detecção:** `Teste Unitário` — Validação de entrada simples (bloqueio de inserção de valores negativos).
* **Impacto no usuário:** Exibição incorreta do saldo do paciente e da clínica.
* **Impacto no negócio:** Ocorrência de erros contábeis, risco de uso indevido do campo financeiro e entraves em auditorias.

---

### Defeito 5 – Controle de Estoque
* **Fase ideal de detecção:** `Teste Unitário` — A regra *"não permitir saída maior que a quantidade disponível"* pode ser isolada em uma função lógica com parâmetros simulados, sem exigir acesso ao banco de dados real.
* **Impacto no usuário:** O profissional pode ficar sem insumos para aplicação de testes psicológicos, mesmo com o sistema indicando disponibilidade.
* **Impacto no negócio:** Decisões de compra equivocadas baseadas em estoque inconsistente, resultando em prejuízo operacional.

---

### Defeito 6 – Exclusão de Paciente
* **Fase ideal de detecção:** `Teste de Integração` — Detectar que a exclusão de um paciente deixa *"consultas órfãs"* exige testar a integração entre os módulos de Paciente e Consulta em conjunto.
* **Impacto no usuário:** Visualização de agendamentos órfãos na agenda sem qualquer associação a um paciente.
* **Impacto no negócio:** Inconsistência de dados no banco, relatórios não confiáveis e alto custo de retrabalho manual para correção retroativa.

---

### Defeito 7 – Pesquisa de Pacientes
* **Fase ideal de detecção:** `Teste Unitário` — A lógica de busca baseada na diferenciação de maiúsculas/minúsculas é facilmente coberta por casos de teste unitários.
* **Impacto no usuário:** Perda de tempo da recepcionista ao não localizar o paciente, embora a integridade do dado não seja afetada.
* **Impacto no negócio:** Baixo impacto direto no faturamento (prioridade baixa), mas prejudica a eficiência do atendimento presencial.

---

### Defeito 8 – Login
* **Fase ideal de detecção:** `Levantamento de Requisitos` — A ausência completa de proteção no mecanismo de autenticação evidencia a falta de especificação de requisitos funcionais de segurança desde a concepção do projeto.
* **Impacto no usuário:** Vulnerabilidade severa em contas de pacientes e profissionais da clínica perante ataques.
* **Impacto no negócio:** Alto risco de vazamento de dados sensíveis de saúde, sanções legais rigorosas e perda irreversível da credibilidade.

---

## Relação com a Curva do Custo de Correção de Defeitos

A análise dos defeitos encontrados no sistema **PsicoCare** exemplifica a aplicação da regra do custo do defeito (*Shift Left*):

* **Baixo Custo de Prevenção (Defeitos 2, 3, 4, 5 e 7):** Trata-se de validações de entrada e regras de negócio locais que deveriam ter sido capturadas em **Testes Unitários** — a etapa mais ágil, isolada e barata para correção.
* **Elevado Custo de Correção (Defeitos 1, 6 e 8):** Vão além de falhas pontuais de código e refletem integrações deficientes e ausência de **Requisitos de Segurança**. Corrigir estas falhas em etapas avançadas ou em produção gera custos elevados, ameaça dados reais de pacientes, expõe a clínica a riscos jurídicos/regulatórios e causa severo dano reputacional.
