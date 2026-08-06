# Atividade Avaliativa: Estratégia de Testes

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 5 |
| **Sistema Analisado** | Clinica PSI |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Elaborar um documento contendo a estratégia definida de testes com base em contexto, riscos e limitações reais.

---

## 1. Estratégia de Testes

> **Objetivo desta seção:** definir quando, como e por que os testes vão acontecer ao longo do projeto, priorizando os pontos de maior risco pro negócio da clínica.

### 1.1 Contexto do projeto

Esses são os pontos de partida que moldam toda a estratégia:

- **Múltiplas funcionalidades principais** (agendamento, prontuário, financeiro, estoque...) → não dá pra testar tudo com a mesma profundidade.
- **Prazo de entrega definido** → o tempo de teste é limitado e precisa ser bem direcionado.
- **Usuários reais** (recepcionistas, psicólogos e, indiretamente, pacientes) → erros afetam o dia a dia de gente de verdade.
- **Time reduzido** → poucas pessoas pra testar tudo; automação ajuda a "esticar" esse tempo.
- **Desenvolvimento ativo** → o sistema está mudando agora, não é algo pronto e parado.
- **Vai sofrer evoluções e correções** → o que funciona hoje precisa continuar funcionando amanhã, mesmo com mudanças constantes.

### 1.2 Quando os testes ocorrem — contínuos ou por fase?

A estratégia é **híbrida**: uma parte dos testes roda continuamente, acompanhando o desenvolvimento; outra parte é concentrada em momentos específicos, geralmente antes de cada entrega.

| Tipo de teste | O que é, resumindo | Quando acontece | Contínuo ou por fase |
|---|---|---|---|
| **Exploratório** | Testar livremente, sem roteiro fixo, procurando comportamentos inesperados | Sempre que uma funcionalidade nova fica pronta | 🔄 Contínuo |
| **Usabilidade** | Avaliar se o sistema é fácil de usar e enxergar | Sempre que uma tela nova ou alterada é entregue | 🔄 Contínuo |
| **Smoke** | Checagem rápida se as funções mais básicas ainda funcionam | A cada novo build/versão | 🔄 Contínuo (e curto) |
| **Sanidade** | Confirmar rápido que uma correção específica funcionou | Logo depois de corrigir um bug | 🔄 Contínuo |
| **Regressão** | Repetir testes já feitos pra garantir que nada quebrou | Antes de cada entrega importante | 📅 Por fase |
| **Sistema** | Testar o fluxo completo, ponta a ponta, integrando os módulos | Antes de cada entrega importante | 📅 Por fase |
| **Performance** | Verificar tempo de resposta com bastante dado/usuário | Em pontos estratégicos (ex: base de dados crescendo) | 📅 Por fase (pontual) |
| **Aceitação** | Validar com quem vai usar de verdade se atende a necessidade | Ao final de cada entrega grande, antes do uso real | 📅 Por fase |

### 1.3 Manual x Automatizado

| Tipo de teste | Manual | Automatizado | Por quê |
|---|---|---|---|
| Exploratório | ✅ | — | Depende de intuição humana pra achar o que um script não prevê |
| Usabilidade | ✅ | Parcial | "Fácil de usar" só um humano avalia bem; ferramenta só checa regra técnica |
| Smoke | — | ✅ | Repetitivo e roda toda hora — ideal pra automatizar |
| Sanidade | ✅ | Parcial | Geralmente é uma checagem pontual e rápida |
| Regressão | — | ✅ | Os mesmos testes se repetem a cada entrega; automatizar economiza tempo do time |
| Sistema | Parcial | Parcial | Fluxo novo é testado manualmente primeiro; quando estabiliza, entra na automação |
| Performance | — | ✅ | Precisa simular carga, o que só ferramenta faz bem |
| Aceitação | ✅ | — | Só quem usa de verdade (a equipe da clínica) pode validar isso |

**Por que essa combinação?** O time é reduzido e o prazo é curto — automatizar o que é repetitivo (smoke e regressão) libera tempo pra focar no que só um humano faz bem: teste exploratório e usabilidade, que foi exatamente onde os bugs mais importantes já apareceram (CT02, CT03, US01 e US02). Como o sistema está em desenvolvimento ativo e vai mudar bastante, a regressão automatizada garante que o que já funciona continue funcionando. E como será usado por pessoas reais, o teste de aceitação com a própria equipe da clínica garante que ele resolve o problema delas na prática, não só "no papel".

### 1.4 Principais riscos do sistema (e como a estratégia reduz cada um)

| Risco | Por que é grave | Como a estratégia reduz esse risco |
|---|---|---|
| **Agendamento duplicado** *(confirmado no CT02)* | Dois pacientes podem ficar marcados no mesmo horário com o mesmo profissional — o mesmo risco pode valer pra salas | Teste exploratório contínuo + teste de sistema focado no fluxo de agendamento |
| **Módulos "desconectados"** *(confirmado no CT03)* | Status não atualiza entre Agendamentos, Check-in e Agenda profissional, gerando retrabalho manual | Teste de sistema ponta a ponta antes de cada entrega, checando a integração entre módulos |
| **Baixo contraste** *(confirmado no US01 e US02)* | Dificulta o uso por pessoas com baixa visão; foge do padrão mínimo (WCAG AA) | Teste de usabilidade contínuo a cada tela nova, com apoio de ferramentas automáticas |
| **Dados sensíveis de pacientes** (Prontuários, Evoluções de sessão) | São dados de saúde mental — sensíveis pela LGPD | Testes de aceitação e de sistema com atenção específica a permissões de acesso |
| **Erros no financeiro** (Recibos, Receitas, Despesas) | Impacto direto no caixa da clínica e em documentos fiscais | Testes funcionais manuais e automatizados nos cálculos e na geração dos documentos |
| **Regressão** (sistema muda o tempo todo) | Uma correção nova pode quebrar algo que já funcionava | Testes de smoke e regressão automatizados, rodando a cada entrega |
| **Prazo curto + time pequeno + várias funcionalidades** | Impossível testar tudo com a mesma profundidade | Priorização por risco (seção 3.6), concentrando esforço manual nos pontos mais críticos |

### 1.5 O que é mais importante garantir

- Que o **fluxo principal da clínica** funcione de ponta a ponta e de forma sincronizada: marcar consulta → confirmar → check-in → evolução de sessão → recibo.
- Que os **dados sensíveis dos pacientes** (prontuários, evoluções de sessão) estejam protegidos e só acessíveis a quem realmente pode ver.
- Que **qualquer pessoa da equipe** consiga usar o sistema com facilidade, incluindo pessoas com baixa visão.

### 1.6 Prioridades: onde focar mais, onde focar menos

| Prioridade | Módulos | Por quê |
|---|---|---|
| **🔴 Alta** | Agendamentos, Reagendamentos, Agenda profissional, Check-in e presença, Salas | Núcleo da operação da clínica; já tem bugs confirmados de conflito e integração (CT02 e CT03) |
| **🔴 Alta** | Prontuários, Evoluções de sessão, Perfis e permissões | Dados de saúde extremamente sensíveis (LGPD); essencial garantir controle de acesso |
| **🟠 Média** | Dashboard, Recibos, Receitas, Despesas, Relatório financeiro | Dashboard já tem bug de contraste confirmado (US01); os demais envolvem dinheiro/documentos fiscais com lógica mais previsível |
| **🟠 Média** | Pacientes, Psicólogos, Funcionários | Cadastros importantes, porém telas mais simples, com menos regras de negócio |
| **🟢 Baixa** | Especialidades, Convênios, Produtos e materiais, Controle de estoque | Informações mais estáticas/administrativas; menor impacto se algo pequeno falhar |

Essa priorização segue o risco: quanto maior o impacto de um erro pro paciente, pro psicólogo ou pra operação da clínica, maior a prioridade do teste. Com time pequeno e prazo definido, focar energia onde o risco é maior é a forma mais eficiente de garantir qualidade sem tentar testar tudo com o mesmo peso.
