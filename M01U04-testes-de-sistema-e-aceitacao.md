# Atividade Avaliativa: Testes de Sistema e de Aceitação — Sistema Bancário

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 3 |
| **Sistema Analisado** | Sistema Bancário — Consulta de Saldo e Autenticação (Cenário Fictício) |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Mapear o cenário de um sistema bancário de consulta de saldo, elaborar casos de Testes de Sistema e de Testes de Aceitação (fluxos principais e alternativos), apresentar justificativas para a classificação dos testes e realizar a revisão por pares de especificações de teste prévias.

---

## Etapa 1: Compreensão do Cenário

O cenário avaliado contempla uma aplicação bancária simplificada em que os clientes realizam autenticação para acessar a conta e visualizar seu saldo corrente.

### 1. Funcionalidades Envolvidas
* **Autenticação de Usuário (Login):** Validação das credenciais do cliente para acesso seguro à conta.
* **Gestão de Sessão e Navegação:** Controle de acesso às áreas restritas do sistema após a autenticação.
* **Consulta e Exibição de Saldo:** Apresentação clara do valor disponível em conta corrente.

### 2. Fluxo Principal (Caminho Feliz)
1. O usuário acessa a tela inicial/login da aplicação bancária.
2. O usuário insere suas credenciais válidas (CPF/Agência/Conta e Senha) e aciona a opção de login.
3. O sistema valida as credenciais, cria a sessão e redireciona o usuário para a tela inicial da conta (Dashboard).
4. O sistema carrega e exibe o saldo atualizado do cliente.

### 3. Variações de Fluxo
* **Máscara de Privacidade do Saldo:** O saldo é exibido oculto por padrão (ex: `R$ ***`), exigindo uma ação do usuário para revelá-lo.
* **Credenciais Incorretas:** Tentativa de acesso com usuário ou senha inválidos, resultando em alerta de erro sem navegar para o dashboard.
* **Acesso Não Autorizado:** Tentativa de acesso direto à tela de saldo sem autenticação prévia, resultando em redirecionamento forçado para a tela de login.
* **Instabilidade de Serviço:** Falha de comunicação com o módulo financeiro ao tentar carregar o saldo após o login.

---

## Etapa 2: Testes de Sistema

Os Testes de Sistema focam no funcionamento integrado da aplicação, na transição entre telas e na navegação de ponta a ponta, sem validar regras de negócio complexas.

### TS-01: Login bem-sucedido e transição para a tela inicial da conta
* **ID:** `TS-01`
* **Título:** Validação da navegação da tela de login para o dashboard após autenticação válida
* **Pré-condições:** Aplicação disponível no ambiente de testes e usuário cadastrado com credenciais ativas.
* **Passos:**
  1. Abrir a aplicação bancária na tela de login.
  2. Preencher os campos de credenciais com dados válidos.
  3. Clicar no botão "Entrar".
* **Resultado Esperado:** O sistema autentica o usuário, encerra a exibição da tela de login e redireciona o fluxo de telas com sucesso para a tela inicial (Dashboard) do cliente.

### TS-02: Carregamento do componente de saldo na interface do dashboard
* **ID:** `TS-02`
* **Título:** Exibição do componente de saldo na tela do dashboard após o login
* **Pré-condições:** Usuário autenticado e com sessão ativa na tela inicial da conta.
* **Passos:**
  1. Observar a área reservada ao resumo financeiro no topo da tela.
  2. Verificar se o valor exibido corresponde aos dados retornados pelo serviço financeiro.
* **Resultado Esperado:** O componente visual referente ao saldo é renderizado corretamente na interface, integrado com o serviço de dados sem falhas de layout.

### TS-03: Bloqueio de navegação e alerta ao informar senha incorreta
* **ID:** `TS-03`
* **Título:** Manutenção do usuário na tela de login ao falhar a autenticação
* **Pré-condições:** Aplicação aberta na tela de login.
* **Passos:**
  1. Digitar o identificador de usuário válido.
  2. Digitar uma senha incorreta.
  3. Clicar no botão "Entrar".
* **Resultado Esperado:** O sistema não realiza a transição de tela, mantém o usuário na tela de login e exibe um componente visual de alerta de erro.

### TS-04: Redirecionamento de segurança para tentativa de acesso direto via URL
* **ID:** `TS-04`
* **Título:** Validação da proteção de rotas privadas sem sessão ativa
* **Pré-condições:** Usuário sem sessão ativa (não autenticado).
* **Passos:**
  1. Abrir o navegador.
  2. Digitar diretamente o endereço/URL da tela de saldo/dashboard.
  3. Pressionar Enter.
* **Resultado Esperado:** O sistema identifica a ausência do token de sessão e redireciona automaticamente a navegação para a tela de login.

### TS-05: Tratamento de falha de comunicação com o módulo financeiro
* **ID:** `TS-05`
* **Título:** Exibição de estado de erro quando o serviço de saldo está indisponível
* **Pré-condições:** Usuário cadastrado com credenciais ativas e ambiente de testes configurado para simular indisponibilidade do módulo financeiro (serviço de saldo).
* **Passos:**
  1. Preencher os campos de credenciais com dados válidos e clicar em "Entrar".
  2. Aguardar o redirecionamento para a tela inicial (Dashboard).
  3. Observar o comportamento da interface diante da falha de comunicação com o serviço de saldo.
* **Resultado Esperado:** O sistema identifica a falha na chamada ao serviço de saldo e renderiza um componente de estado de erro na interface, sem travar, sem quebrar o layout e sem exibir dados inconsistentes ou desatualizados.

---

## Etapa 3: Testes de Aceitação

Os Testes de Aceitação focam na perspectiva do usuário final e no valor entregue pelo negócio, assegurando que as expectativas de usabilidade, clareza e privacidade sejam atendidas.

### TA-01: Exibição clara e legível do saldo disponível para o cliente
* **ID:** `TA-01`
* **Título:** Consulta imediata do saldo bancário com clareza visual para o cliente
* **Pré-condições:** Cliente possui conta bancária ativa e credenciais válidas cadastradas.
* **Passos:**
  1. Efetuar login no aplicativo com credenciais válidas.
  2. Acessar a tela inicial da conta.
* **Resultado Esperado:** O cliente visualiza o valor do seu saldo disponível em moeda corrente (ex: R$ 1.250,00) de forma destacada e compreensível, atendendo à necessidade de transparência financeira sem etapas adicionais.

### TA-02: Controle de privacidade para exibição/ocultação do saldo
* **ID:** `TA-02`
* **Título:** Alternância do modo de privacidade do saldo em ambientes públicos
* **Pré-condições:** Cliente autenticado na tela inicial da conta.
* **Passos:**
  1. Observar o saldo exibido em formato mascarado (`R$ ***`).
  2. Clicar no ícone de "revelar saldo" (ícone de olho).
  3. Clicar novamente no ícone para ocultar o saldo.
* **Resultado Esperado:** O aplicativo alterna entre ocultar e exibir os valores numéricos com precisão, permitindo que o cliente consulte seus dados financeiros com segurança em locais públicos.

### TA-03: Comunicação clara e amigável em caso de falha de login
* **ID:** `TA-03`
* **Título:** Alerta intuitivo ao cliente em caso de erro na digitação dos dados
* **Pré-condições:** Cliente na tela de login.
* **Passos:**
  1. Inserir credenciais incorretas.
  2. Acionar a opção "Entrar".
* **Resultado Esperado:** O cliente recebe uma mensagem amigável e explicativa na tela (ex: "Usuário ou senha incorretos. Verifique seus dados e tente novamente"), evitando termos técnicos frustrantes.

### TA-04: Mensagem orientadora durante indisponibilidade do serviço de saldo
* **ID:** `TA-04`
* **Título:** Feedback transparente durante instabilidade momentânea na consulta de saldo
* **Pré-condições:** Cliente autenticado na conta durante período de manutenção da camada de saldo.
* **Passos:**
  1. Acessar a tela do dashboard da conta durante indisponibilidade do serviço de saldo.
* **Resultado Esperado:** O cliente visualiza uma mensagem clara e tranquilizadora (ex: "Não foi possível carregar seu saldo no momento devido a uma instabilidade temporária em nosso sistema. Tente novamente em instantes"), garantindo que o usuário compreenda o motivo da falha temporária.

---

## Etapa 4: Justificativa e Classificação

| ID do Teste | Tipo de Teste | Por que é um Teste de Sistema? | Por que é um Teste de Aceitação? |
| :--- | :--- | :--- | :--- |
| **TS-01** | Sistema | Valida a integração completa entre a tela de login, o serviço de autenticação e o redirecionamento para a tela inicial. | N/A (Foco estritamente na navegação e funcionamento técnico integrado do software). |
| **TS-02** | Sistema | Assegura que o componente visual do saldo se conecta corretamente ao serviço de dados e carrega na interface sem falhas. | N/A (Foco na renderização e integração técnica do componente). |
| **TS-03** | Sistema | Testa a resposta do sistema diante de um erro de autenticação, confirmando o bloqueio de rota e a exibição do alerta. | N/A (Valida a regra de segurança e o controle de navegação do sistema). |
| **TS-04** | Sistema | Valida a arquitetura de proteção de rotas da aplicação, garantindo que URLs restritas exijam token de sessão. | N/A (Foco no comportamento da infraestrutura de segurança do sistema). |
| **TS-05** | Sistema | Valida a resiliência da aplicação diante de uma falha de integração com o módulo financeiro, garantindo que o erro seja tratado sem quebrar a interface. | N/A (Foco no comportamento técnico do sistema diante da falha, não na qualidade da comunicação ao cliente). |
| **TA-01** | Aceitação | N/A (Não busca validar apenas se a tela carrega, mas a qualidade e utilidade do dado entregue). | Valida se a necessidade do cliente (saber quanto dinheiro possui) é atendida de forma clara e imediata na primeira tela. |
| **TA-02** | Aceitação | N/A (A alternância visual é apenas o meio; o foco é a experiência do usuário). | Garante o valor de negócio relacionado à privacidade do cliente ao usar o aplicativo em locais públicos. |
| **TA-03** | Aceitação | N/A (Não avalia apenas o código de erro, mas a linguagem utilizada com o usuário). | Assegura que a mensagem de erro seja compreensível para o cliente final, mantendo uma boa usabilidade. |
| **TA-04** | Aceitação | N/A (Avalia o tratamento da expectativa do usuário em momentos de falha). | Evita o pânico do cliente e garante uma comunicação transparente sobre o estado do seu dinheiro. |
