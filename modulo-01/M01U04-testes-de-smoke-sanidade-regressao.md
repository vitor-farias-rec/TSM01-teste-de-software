# Atividade Avaliativa: Testes de Smoke, Sanidade e Regressão

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 4 |
| **Sistema Analisado** | Nova versão de Sistema Bancário (Cenário Fictício) |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Propor 5 cenários de teste para as modalidades de Smoke, Sanidade e Regressão, com base na nova versão do sistema bancário que trouxe alterações no login e no saldo. Além disso, a entrega inclui as justificativas que fundamentam a escolha dos cenários para cada tipo de teste.

---

##  Teste de Smoke

> Verifica se o sistema está com suas funcionalidades estáveis para outros testes, cobrindo especialmente as críticas e executado após deploy e nova build.

### Cenários de Teste

| ID | Cenário de Teste | Ação / Objetivo |
| :---: | :--- | :--- |
| **ST-01** | Renderização da Tela de Login | Verificar se a tela de login abre sem erros ao acessar o sistema. |
| **ST-02** | Autenticação Válida | Confirmar o login utilizando usuário e senha válidos. |
| **ST-03** | Carregamento da Tela Inicial | Confirmar se a tela inicial carrega corretamente após o login. |
| **ST-04** | Presença do Componente de Saldo | Verificar se o saldo aparece na tela inicial (Não verifica o valor exato). |
| **ST-05** | Encerramento de Sessão (Logout) | Verificar se é possível fazer logout do sistema com sucesso. |

###  Justificativas dos Cenários
* **ST-01:** Garante que a tela de login está acessível após o deploy.
* **ST-02:** Valida o fluxo básico de acesso para ser possível executar novos testes.
* **ST-03:** Garante que o redirecionamento pós-login não resulta em tela em branco ou erro.
* **ST-04:** Confirma visualmente que o elemento modificado nesta versão está sendo renderizado na interface.
* **ST-05:** Valida a integridade do ciclo completo da sessão (entrada, carregamento e saída).

> **Por que esse conjunto?**  
> Como o login e a tela inicial foram alterados, o Teste de Smoke precisa garantir que o caminho mais básico (logar, ver a tela inicial e sair) está funcionando. Se algum desses passos falhar, a versão deve ser rejeitada imediatamente antes de gerar retrabalho com novos testes.

---

##  Teste de Sanidade

> Verificar se uma funcionalidade específica, após alteração, está funcionando corretamente, isto é, também foca em estabilidade, mas após um ajuste pontual ou correção de bug.

### Cenários de Teste

| ID | Cenário de Teste | Ação / Objetivo |
| :---: | :--- | :--- |
| **SN-01** | Liberação de Acesso com Dados Corretos | Confirmar que o login com credenciais válidas libera o acesso com sucesso. |
| **SN-02** | Bloqueio de Credenciais Incorretas | Testar o login com senha errada e confirmar a mensagem de erro. |
| **SN-03** | Exibição correta do Saldo | Conferir se o saldo exibido na tela inicial é exatamente igual ao saldo real da conta. |
| **SN-04** | Atualização Dinâmica do Saldo | Fazer uma movimentação, como, por exemplo, uma transferência pix, e conferir se o saldo é atualizado na hora. |
| **SN-05** | Formatação de Dados Numéricos | Conferir se o saldo é exibido no formato correto (moeda R$, casas decimais e sinal negativo ou positivo conforme ação tomada). |

###  Justificativas dos Cenários
* **SN-01:** Valida diretamente se a correção do bug de login funcionou como esperado no fluxo correto.
* **SN-02:** Garante que a correção no login não comprometeu as regras de validação e segurança.
* **SN-03:** Valida se o ajuste na exibição reflete o dado correto do banco de dados sem distorção.
* **SN-04:** Garante que o novo componente de saldo reage corretamente às alterações de estado em tempo real.
* **SN-05:** Valida se os ajustes visuais de formatação foram aplicados corretamente no componente.

> **Por que esse conjunto?**  
> Estes cenários focam exatamente nos dois pontos de mudança da versão. O objetivo é confirmar que a correção do login e a nova exibição do saldo funcionam perfeitamente no detalhe, sem defeitos imediatos nas próprias telas alteradas.

---

##  Teste de Regressão

> Garante que as funcionalidades existentes não foram afetadas por mudanças recentes, o que cobre múltiplos fluxos e necessita ser executado após novas funcionalidades serem implementadas.

### Cenários de Teste

| ID | Cenário de Teste | Ação / Objetivo |
| :---: | :--- | :--- |
| **RG-01** | Login com Múltiplos Perfis | Testar login com diferentes perfis de usuário (comum, admin, PJ). |
| **RG-02** | Fluxo de Recuperação de Senha | Testar a funcionalidade de esqueci minha senha e alteração de senha. |
| **RG-03** | Consistência do Extrato Bancário | Conferir se o extrato de transações continua exibindo os valores e históricos corretos. |
| **RG-04** | Saldo em Telas Secundárias | Conferir se o saldo aparece correto em outras telas, como, por exemplo, a tela inicial ao clicar na máscara do ícone de exibição de em formato de olho.  |
| **RG-05** | Trava de Transferência por Saldo | Testar uma transferência com valor superior ao saldo e validar o bloqueio. |

### Justificativas dos Cenários
* **RG-01:** Garante que a alteração no código do login não afetou o controle de permissões por perfil.
* **RG-02:** Valida se módulos próximos ao login continuam operando sem falhas derivadas da alteração.
* **RG-03:** Assegura que ajustes na exibição do saldo na home não corromperam a consulta de histórico de transações.
* **RG-04:** Evita divergências de dados entre diferentes telas da aplicação que consomem a mesma informação.
* **RG-05:** Garante que a regra de negócio de bloqueio financeiro continua ativa e funcional no sistema.

> **Por que esse conjunto?**  
> Login e saldo são informações vitais e interligadas com diversos módulos do sistema bancário (como extrato, transferências e segurança). O teste de regressão garante que a mexida nessas duas partes não gerou "efeitos colaterais" em funcionalidades que já estavam estáveis.
