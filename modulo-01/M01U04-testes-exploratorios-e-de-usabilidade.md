# Atividade Avaliativa: Testes Exploratórios e de Usabilidade

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 4 |
| **Sistema Analisado** | Clinica PSI |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Em Execução |

---

> **Objetivo da Atividade:**  
> Propor a exploração livre de 5 cenários do sistema e o mapeamento de 5 potenciais problemas de usabilidade, detalhando como essas falhas impactam a experiência do usuário.

---

## 1. Testes Exploratórios

Em um teste exploratório, o objetivo é avaliar o comportamento da aplicação em cenários reais de uso, testando fluxos principais, regras de negócio e limites do sistema.

### Pontos para Explorar:

1. **[CT01] Mecanismo de Busca (`Pesquisar registros...`)**
   * **O que testar:** Digitar nomes parciais de psicólogos, datas ou status (ex: "10:30").
   * **Comportamento esperado:** A busca deve responder em tempo real, sem travar ou quebrar caso sejam digitados caracteres especiais.
   * * **Status:** 🟢 **Aprovado**

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT01)</b></summary>

   <br>
   
   https://github.com/user-attachments/assets/b41ec11f-3698-4ae5-9a9b-73e62ed9cb0c

   </details>

2. **[CT02] Validação de Conflito de Horários (`+ Novo registro`)**
   * **O que testar:** Tentar agendar uma nova consulta para o mesmo profissional no mesmo dia e horário de um agendamento já existente (ex: Dra. Juliana Martins no dia 2026-07-20 às 09:00).
   * **Comportamento esperado:** O sistema deve emitir um alerta de conflito e bloquear o agendamento duplo.
   * **Status:** 🔴 **Reprovado** *(O sistema permitiu o agendamento duplicado sem exibir alerta de conflito)*

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT02)</b></summary>

   <br>
   
   https://github.com/user-attachments/assets/9192c3e9-bc54-4460-ac10-66ef29e1eb4a

   </details>

3. **[CT03] Integração das Ações da Tabela ('✎ ⌫')**
   * **O que testar:** Clicar nos ícones da coluna **Ações** para editar um registro e alterar o status de "Pendente" para "Confirmado".
   * **Comportamento esperado:** A alteração deve ser refletida imediatamente na tabela e refletir em outras áreas do sistema (como no módulo *Check-in e presença* e na *Agenda profissional*).
   * **Status:** 🔴 **Reprovado** *(Falha de integração entre módulos: a alteração do status para "Confirmado" é salva na tabela, porém não é refletida nos módulos "Check-in e presença" e "Agenda profissional", exigindo o cadastro manual e duplicado nas outras telas).*

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT03)</b></summary>

   <br>
   
   https://github.com/user-attachments/assets/b856d392-4fbe-4e10-8c80-d3a761487ee5

   </details>

4. **[CT04] Validação de Campos Obrigatórios (`+ Novo registro`)**
   * **O que testar:** Tentar salvar um novo agendamento deixando campos essenciais em branco (ex: Data ou Status).
   * **Comportamento esperado:** O sistema deve impedir o salvamento e indicar claramente quais campos precisam ser preenchidos.
   * **Status:** 🟢 **Aprovado**

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT04)</b></summary>

   <br>
   
   https://github.com/user-attachments/assets/0632b84d-ccb3-4afa-8e21-c69f1ee207f5

   </details>

5. **[CT05] Feedback de Lista Vazia (`Pesquisar registros...`)**
   * **O que testar:** Digitar um termo ou nome inexistente na barra de pesquisa (ex: "Estudante").
   * **Comportamento esperado:** O sistema deve exibir uma mensagem clara e amigável informando que nenhum registro foi encontrado, em vez de deixar a tabela travada ou em branco sem aviso.
   * **Status:** 🟢 **Aprovado**

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT05)</b></summary>

   <br>
   
   https://github.com/user-attachments/assets/257f8e6d-f8a9-4e6f-9fe6-13ee19bda056

   </details>

## 2. Testes de Usabilidade

Avalia a facilidade e praticidade do sistema na perspectiva do usuário, levando em conta, inclusive aspectos de visibilidade e legibilidade também.

1. **[US01] Botão de Atalho no Dashboard (`+Cadastrar Paciente`)**
   * **O que testar:** Aceitação do padrão internacional WCAG a respeito da visibilidade (ex: Paleta de cores do fundo ).
   * **Comportamento esperado:** O contraste entre o texto e os elementos da interface deve estar, no mínimo, no padrão AA para que o usuário possa enxergar com clareza o botão.
   * * **Status:** 🔴 **Reprovado** *(Proporção de contraste entre o elemento o texto pequeno do botão e a paleta de cores dele em relação ao fundo da tela está em _____).
    
   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT05)</b></summary>

   <br>
   
   VIDEO

   </details>

2. **[US01] Botão de Atalho no Dashboard (`+Cadastrar Paciente`)**
   * **O que testar:** Aceitação do padrão internacional WCAG a respeito da visibilidade (ex: Paleta de cores do fundo ).
   * **Comportamento esperado:** O contraste entre o texto e os elementos da interface deve estar, no mínimo, no padrão AA para que o usuário possa enxergar com clareza o botão.
   * * **Status:** 🔴 **Reprovado** *(Proporção de contraste entre o elemento o texto pequeno do botão e a paleta de cores dele em relação ao fundo da tela está em _____).
    
   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT05)</b></summary>

   <br>
   
   VIDEO

   </details>
