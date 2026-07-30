# Atividade Avaliativa: Testes Não Funcionais — Plataforma de Agendamento de Consultas

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 3 |
| **Sistema Analisado** | Plataforma de Agendamento de Consultas (Cenário Fictício / Estudo de Caso de Aula) |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Elaborar um checklist de testes não funcionais para o sistema proposto, cobrindo obrigatoriamente os pilares de **Performance**, **Segurança**, **Usabilidade** e **Compatibilidade**, detalhando para cada item o que será verificado e os riscos associados à ausência da validação.

---

## Checklist de Testes Não Funcionais

| Categoria | Item do Checklist | O que será Verificado | Risco Associado |
| :--- | :--- | :--- | :--- |
| **Performance** | Uso simultâneo por múltiplos usuários durante horários de pico | Estabilidade do sistema com múltiplos usuários agendando ao mesmo tempo | Lentidão justamente nos horários de maior demanda |
| **Performance** | Não é permitido agendar dois horários simultâneos para o mesmo usuário | O que acontece quando duas requisições do mesmo usuário chegam quase ao mesmo tempo | Falha de gerar dois agendamentos quando duas requisições simultâneas do mesmo usuário conflitam |
| **Performance** | Consulta de especialidades e profissionais disponíveis | Tempo de resposta da busca por especialidades e profissionais | Lentidão da busca pode desencorajar o usuário a realizar o agendamento |
| **Segurança** | Dados pessoais devem ser protegidos conforme boas práticas de segurança | Técnica de proteção de dados e o armazenamento de dados como nome, CPF e endereço | Vazamento de dados sensíveis e violação à LGPD |
| **Segurança** | Cadastro e autenticação de usuários | Processo de login (senha, bloqueio após tentativas incorretas, proteção da sessão) | Invasão de contas por ataques de phishing |
| **Segurança** | Usuários devem estar autenticados para agendar consultas | Se o sistema realmente bloqueia o agendamento para quem não está logado | Agendamento feito por usuário não identificado |
| **Usabilidade** | Cancelamentos só podem ocorrer até 24h antes da consulta | Se a interface deixa claro que há um prazo de 24h para que o usuário possa realizar um cancelamento | Frustração do usuário ao tentar cancelar fora do prazo sem entender o motivo |
| **Usabilidade** | Área administrativa para gestão de horários e atendimentos | Facilidade de uso da área administrativa no dia a dia dos gestores | Erros operacionais na gestão de horários e atendimentos por dificuldade de manuseio |
| **Usabilidade** | Agendamento, cancelamento e visualização de consultas | Clareza e simplicidade do fluxo dessas ações para o usuário final | Desistência do uso ou erro no agendamento por interface confusa |
| **Compatibilidade** | Sistema acessado via navegador web | Funcionamento correto em diferentes navegadores | Falha de acesso para usuários de navegadores não testados |
| **Compatibilidade** | Notificações de confirmação de agendamento | Entrega correta das notificações no dispositivo de acesso | Usuário não recebe a confirmação e perde a consulta por falta de lembrete |
| **Compatibilidade** | Usuários podem acessar por desktop, tablet ou celular | Responsividade da interface em diferentes tamanhos de tela e sistemas operacionais | Usuário mobile não consegue concluir o agendamento por quebra de layout |

---

## Detalhamento das Categorias Exigidas

### 1. Performance
* **Carga e Estabilidade:** Valida a capacidade de atendimento durante picos de tráfego sem degradação do serviço.
* **Concorrência (Race Condition):** Garante que duas requisições simultâneas não gerem duplicidade de agendamento no banco de dados.
* **Tempo de Resposta:** Garante tempos de resposta rápidos nas buscas para evitar perda de conversão.

---

### 2. Segurança
* **Proteção de Dados Sensíveis:** Assegura conformidade com a LGPD no tratamento e armazenamento de informações pessoais.
* **Autenticação e Sessão:** Avalia políticas de senha, mitigação de força bruta e proteção de tokens de acesso.
* **Controle de Acesso:** Garante que rotas críticas da aplicação estejam restritas a usuários autenticados.

---

### 3. Usabilidade
* **Transparência de Regras:** Garante a exibição clara de prazos e políticas de cancelamento para o usuário.
* **Eficiência Operacional:** Foca na facilidade e baixa taxa de erro na interface utilizada pelos gestores.
* **Jornada do Usuário:** Avalia se o fluxo principal (agendamento e consulta) é intuitivo e acessível.

---

### 4. Compatibilidade
* **Suporte Multi-Navegadores:** Garante comportamento consistente nos principais navegadores do mercado.
* **Comunicação por Notificações:** Garante o recebimento adequado de confirmações no dispositivo do usuário.
* **Responsividade Multi-Dispositivo:** Assegura adaptação correta de layout e navegação em telas mobile, tablets e desktops.
