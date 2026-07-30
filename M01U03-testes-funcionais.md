# Atividade Avaliativa: Testes Funcionais — Sistema de Gerenciamento de Pedidos (SGP)

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 3 |
| **Sistema Analisado** | SGP — Sistema de Gerenciamento de Pedidos (Cenário Fictício) |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Mapear e classificar as funcionalidades, regras de negócio e integrações da aplicação web **Sistema de Gerenciamento de Pedidos (SGP)** — apresentada em especificação fictícia de aula — nos respectivos níveis de teste (Unitário, Integração e Sistema), fornecendo a justificativa técnica para cada cenário.

---

## Tabela Resumo da Classificação dos Testes

| Caso de Teste / Funcionalidade | Nível de Teste | Foco Principal da Validação |
| :--- | :--- | :--- |
| O pedido deve conter pelo menos um item | Unitário | Validação direta de regra de dados isolada. |
| O valor total deve considerar quantidade e preço dos produtos | Unitário | Aplicação correta da fórmula matemática isolada. |
| Cadastro e autenticação de usuários | Integração | Comunicação entre cadastro, autenticação e banco de dados. |
| Consulta de produtos disponíveis | Integração | Comunicação entre a busca da aplicação e o banco do inventário. |
| Adição e remoção de itens no carrinho | Integração | Alinhamento do módulo de pedidos/pagamento com perfis de acesso. |
| Cálculo automático do valor total do pedido | Integração | Validação isolada de fluxo de itens com parâmetros conhecidos. |
| Usuários não autenticados não podem realizar pedidos | Integração | Comunicação entre o serviço de pedidos e o serviço de autenticação. |
| Após a confirmação, o pedido não pode ser alterado | Integração | Comunicação entre validação de ações e o módulo de armazenamento. |
| Integração com banco de dados de produtos | Integração | Consulta e recebimento de produto, preço e estoque no banco. |
| Integração com serviço de autenticação | Integração | Delegação de credenciais, sessão e perfis a serviço dedicado. |
| Integração com serviço de pedidos | Integração | Troca consistente de dados de criação, status e valores. |
| Finalização do pedido com confirmação | Sistema | Fluxo ponta a ponta envolvendo autenticação, itens e pagamento. |

---

## Detalhamento e Justificativas Técnicas

### 1. Testes de Nível Unitário

#### Teste: O pedido deve conter pelo menos um item
* **Nível:** `Unitário`
* **Justificativa:** O teste valida diretamente os dados e as regras do objeto de pedido. É possível utilizá-lo com dados fictícios de forma isolada, sem necessidade de consultar banco de dados ou serviço de autenticação.

#### Teste: O valor total deve considerar quantidade e o preço dos produtos
* **Nível:** `Unitário`
* **Justificativa:** O teste confirma a correta aplicação da fórmula matemática a partir de combinações fictícias de quantidades e preços variados, dispensando integrações com banco de dados ou sistemas externos.

---

### 2. Testes de Nível de Integração

#### Teste: Cadastro e autenticação de usuários
* **Nível:** `Integração`
* **Justificativa:** O sistema possui estratificação de perfis de acesso (clientes, colaboradores e gestor) e armazena dados de pessoas físicas no banco de dados. A validação depende da comunicação efetiva entre os módulos de cadastro, autenticação e o banco de dados.

#### Teste: Consulta de produtos disponíveis
* **Nível:** `Integração`
* **Justificativa:** Exige verificar se o mecanismo de busca se comunica corretamente com o banco de dados de inventário e se os parâmetros de quantidade e detalhes do produto são retornados conforme solicitado.

#### Teste: Adição e remoção de itens no carrinho
* **Nível:** `Integração`
* **Justificativa:** Avalia a interação do módulo de pedidos e pagamento com os diferentes perfis de acesso do sistema, garantindo que as ações permitidas estejam alinhadas com as permissões de cada usuário.

#### Teste: Cálculo automático do valor total do pedido
* **Nível:** `Integração`
* **Justificativa:** Teste focado em processar itens com quantidades e preços conhecidos, garantindo a consistência das estruturas de dados sem sobrecarregar a rotina com dependências desnecessárias do banco de dados.

#### Teste: Usuários não autenticados não podem realizar pedidos
* **Nível:** `Integração`
* **Justificativa:** Depende da comunicação direta entre dois serviços distintos: o serviço de pedidos precisa consultar o serviço de autenticação para validar o perfil e bloquear usuários sem credenciais válidas.

#### Teste: Após a confirmação, o pedido não pode ser alterado
* **Nível:** `Integração`
* **Justificativa:** O teste simula a tentativa de alteração em um pedido já confirmado e valida se o serviço de pedidos rejeita a operação consultando o status armazenado no módulo de persistência.

#### Teste: Integração com banco de dados de produtos
* **Nível:** `Integração`
* **Justificativa:** Valida a comunicação direta entre a aplicação e a camada de dados, garantindo que informações de produto, preço e estoque sejam consultadas e recebidas corretamente.

#### Teste: Integração com serviço de autenticação
* **Nível:** `Integração`
* **Justificativa:** Confirma que a aplicação delega a autenticação de forma consistente a um serviço dedicado, validando a criação de sessão e o retorno do perfil do usuário.

#### Teste: Integração com serviço de pedidos
* **Nível:** `Integração`
* **Justificativa:** Assegura que o SGP envia e recebe informações de criação, status e valores de pedidos de um serviço centralizado sem gerar inconsistências nos dados.

---

### 3. Testes de Nível de Sistema

#### Teste: Finalização do pedido com confirmação
* **Nível:** `Sistema`
* **Justificativa:** Trata-se de um teste ponta a ponta (E2E) que engloba múltiplos componentes do SGP em funcionamento conjunto: autenticação válida de usuário, presença de pelo menos um item no carrinho, cálculo correto do valor total e a confirmação final da transação.
