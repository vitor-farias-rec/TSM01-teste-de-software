# Atividade Avaliativa: Estruturando Casos de Teste — Tela de Login

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 4 |
| **Sistema Analisado** | Tela de Login e Autenticação de Usuários (Cenário Fictício) |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Elaborar uma suíte com no mínimo 10 casos de teste completos para a funcionalidade de Login, estruturados com ID, Título, Pré-condições, Passos e Resultado Esperado, contemplando tanto o caminho feliz quanto cenários alternativos e de exceção.

---

## Tabela Resumo da Suíte de Testes

| ID | Título do Caso de Teste | Tipo de Fluxo | Foco do Teste |
| :--- | :--- | :--- | :--- |
| **TC-01** | Login bem-sucedido com e-mail e senha válidos | Caminho Feliz | Autenticação e acesso à aplicação |
| **TC-02** | Redirecionamento para redefinição via "Esqueci minha senha" | Caminho Feliz | Recuperação de acesso ao usuário |
| **TC-03** | Tentativa de login com senha incorreta | Alternativo | Validação de credenciais e mensagem de erro |
| **TC-04** | Tentativa de login com e-mail não cadastrado | Alternativo | Tratamento de usuário inexistente no banco |
| **TC-05** | Tentativa de submissão com campos obrigatórios vazios | Alternativo / Exceção | Validação de formulário na camada visual |
| **TC-06** | Inserção de e-mail em formato sintaticamente inválido | Alternativo / Exceção | Validação do formato do campo de entrada |
| **TC-07** | Bloqueio de conta após 3 tentativas consecutivas incorretas | Segurança / Regra | Proteção contra ataques de força bruta |
| **TC-08** | Alternância da visibilidade da senha (Exibir/Ocultar) | Usabilidade / UI | Controle visual do campo de senha |
| **TC-09** | Remoção de espaços em branco acidentais no e-mail (Trimming) | Caso Borda | Tratamento e higienização de inputs |
| **TC-10** | Prevenção de submissão duplicada por múltiplos cliques rápidos | Performance / UI | Bloqueio do botão no estado de carregamento |

---

## Detalhamento dos Casos de Teste

### 1. Fluxos Principais (Caminho Feliz)

#### TC-01: Login bem-sucedido com e-mail e senha válidos
* **ID:** `TC-01`
* **Título:** Autenticação de usuário com credenciais válidas
* **Pré-condições:** Usuário cadastrado no sistema com e-mail `cliente@email.com` e senha `Senha@123`. Aplicação aberta na tela de login.
* **Passos:**
  1. Clicar no campo de texto "E-mail".
  2. Digitar `cliente@email.com`.
  3. Clicar no campo de texto "Senha".
  4. Digitar `Senha@123`.
  5. Clicar no botão "Entrar".
* **Resultado Esperado:** O sistema valida as credenciais, encerra a exibição da tela de login, gera o token de sessão e redireciona o usuário para a tela inicial (Dashboard) da conta.

#### TC-02: Redirecionamento para redefinição via "Esqueci minha senha"
* **ID:** `TC-02`
* **Título:** Acesso à tela de recuperação de senha
* **Pré-condições:** Aplicação aberta na tela de login. O botão/link "Esqueci minha senha" está visível na interface.
* **Passos:**
  1. Clicar no link "Esqueci minha senha".
* **Resultado Esperado:** O sistema redireciona o usuário para a página de recuperação de acesso, exibindo o campo para digitação do e-mail de redefinição.

---

### 2. Fluxos Alternativos e de Exceção

#### TC-03: Tentativa de login com senha incorreta
* **ID:** `TC-03`
* **Título:** Bloqueio de acesso com senha divergente
* **Pré-condições:** Usuário `cliente@email.com` cadastrado no sistema. Aplicação aberta na tela de login.
* **Passos:**
  1. Inserir `cliente@email.com` no campo "E-mail".
  2. Inserir `SenhaErrada99` no campo "Senha".
  3. Clicar no botão "Entrar".
* **Resultado Esperado:** O sistema não realiza o login, permanece na página atual e exibe a mensagem de alerta: "E-mail ou senha incorretos".

#### TC-04: Tentativa de login com e-mail não cadastrado
* **ID:** `TC-04`
* **Título:** Tentativa de autenticação com usuário inexistente
* **Pré-condições:** O e-mail `nao_existente@email.com` não possui cadastro no banco de dados.
* **Passos:**
  1. Inserir `nao_existente@email.com` no campo "E-mail".
  2. Inserir `QualquerSenha123` no campo "Senha".
  3. Clicar no botão "Entrar".
* **Resultado Esperado:** O login é recusado e o sistema exibe a mensagem genérica de segurança: "E-mail ou senha incorretos".

#### TC-05: Tentativa de submissão com campos obrigatórios vazios
* **ID:** `TC-05`
* **Título:** Submissão do formulário de login com campos em branco
* **Pré-condições:** Aplicação aberta na tela de login. Campos "E-mail" e "Senha" vazios.
* **Passos:**
  1. Deixar os campos "E-mail" e "Senha" sem preenchimento.
  2. Clicar diretamente no botão "Entrar".
* **Resultado Esperado:** O formulário não envia a requisição e exibe mensagens de validação abaixo dos respectivos campos: "O campo e-mail é obrigatório" e "O campo senha é obrigatório".

#### TC-06: Inserção de e-mail em formato sintaticamente inválido
* **ID:** `TC-06`
* **Título:** Validação da sintaxe do campo de e-mail
* **Pré-condições:** Aplicação aberta na tela de login.
* **Passos:**
  1. Inserir o texto `usuario_sem_arroba.com` no campo "E-mail".
  2. Inserir uma senha qualquer no campo "Senha".
  3. Clicar no botão "Entrar".
* **Resultado Esperado:** O sistema identifica a falta do caractere `@` ou formato válido de e-mail, impede a submissão e exibe o alerta: "Por favor, insira um e-mail válido".

---

### 3. Cenários de Segurança, Usabilidade e Casos de Borda)

#### TC-07: Bloqueio de conta após 3 tentativas consecutivas incorretas
* **ID:** `TC-07`
* **Título:** Bloqueio temporário de conta por excesso de falhas de autenticação
* **Pré-condições:** Usuário `cliente@email.com` ativo no sistema. Limite máximo configurado para 3 tentativas malsucedidas.
* **Passos:**
  1. Inserir `cliente@email.com` e a senha incorreta `Errada1`. Clicar em "Entrar".
  2. Inserir a senha incorreta `Errada2`. Clicar em "Entrar".
  3. Inserir a senha incorreta `Errada3`. Clicar em "Entrar".
* **Resultado Esperado:** Na 3ª tentativa, o sistema bloqueia o acesso à conta e exibe o alerta: "Sua conta foi temporariamente bloqueada por segurança devido ao excesso de tentativas incorretas. Tente novamente em 15 minutos".

#### TC-08: Alternância da visibilidade da senha (Exibir/Ocultar)
* **ID:** `TC-08`
* **Título:** Ocultação e revelação dos caracteres do campo de senha
* **Pré-condições:** Aplicação aberta na tela de login com o campo de senha preenchido com `SenhaSecret123`.
* **Passos:**
  1. Verificar que os caracteres do campo de senha estão mascarados em formato de bolinhas/asteriscos.
  2. Clicar no ícone de "olho" (Exibir senha) localizado dentro do campo de senha.
  3. Verificar se o texto `SenhaSecret123` fica visível em texto simples.
  4. Clicar novamente no ícone de "olho" (Ocultar senha).
* **Resultado Esperado:** O campo alterna corretamente entre o tipo `password` (caracteres mascarados) e o tipo `text` (caracteres visíveis), permitindo que o usuário confira o que digitou.

#### TC-09: Remoção de espaços em branco acidentais no e-mail (Trimming)
* **ID:** `TC-09`
* **Título:** Tratamento de espaços antes e depois do e-mail (*Trimming*)
* **Pré-condições:** Usuário cadastrado com o e-mail `cliente@email.com` e senha `Senha@123`.
* **Passos:**
  1. Inserir no campo "E-mail" o texto com espaços extras: `   cliente@email.com   `.
  2. Inserir a senha correta `Senha@123`.
  3. Clicar no botão "Entrar".
* **Resultado Esperado:** O sistema realiza a higienização automática do input (remoção dos espaços nas extremidades) e efetua o login com sucesso no dashboard.

#### TC-10: Prevenção de submissão duplicada por múltiplos cliques rápidos
* **ID:** `TC-10`
* **Título:** Desativação do botão "Entrar" durante o processamento da requisição
* **Pré-condições:** Aplicação aberta na tela de login com credenciais preenchidas. Conexão simulada com latência de rede.
* **Passos:**
  1. Clicar rapidamente 3 vezes seguidas no botão "Entrar".
* **Resultado Esperado:** Ao primeiro clique, o botão "Entrar" assume o estado desabilitado (`disabled`), exibe um indicador visual de carregamento (*spinner*) e impede o envio de requisições duplicadas ao servidor.
