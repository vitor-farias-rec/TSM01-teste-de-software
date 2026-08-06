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

1. **[US01] Constraste visual do botão (`+Cadastrar Paciente`)**
   * **O que testar:** nível de contraste entre a cor do texto e o fundo do botão principal (`+ Cadastrar Paciente`) em relação ao fundo da tela, com base nas diretrizes internacionais de acessibilidade WCAG (nível AA).
   * **Comportamento esperado:** botão principal deve ter um nível de contraste mínimo de 4.5:1 em relação ao fundo para garantir leitura fácil por qualquer pessoa.
   * * **Status:** 🔴 **Reprovado** *(A combinação do azul do botão com o texto pequeno em branco apresenta taxa de contraste abaixo do recomendado pelo padrão WCAG 2.1 AA, dificultando a leitura rápida).
    
   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (CT05)</b></summary>

   <br>
   
   VIDEO_US02.mp4

   </details>

2. **[US02] Dica de Tela nos Ícones de Ação ('✎ ⌫')**
   * **O que testar:** Verificar se o sistema exibe uma legenda informativa quando o usuário passa o ponteiro do mouse sobre os ícones da coluna **Ações**.
   * **Comportamento esperado:** Ao posicionar o mouse sobre o lápis ou sobre o ícone de remoção, deve aparecer um pequeno balão de texto indicando a função de cada um (ex: "Editar agendamento" e "Excluir agendamento").
   * **Status:** 🔴 **Reprovado** *(Nenhuma legenda explicativa surge ao passar o mouse sobre os ícones, o que pode causar dúvidas na recepção sobre o significado exato dos símbolos).*

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (US02)</b></summary>

   <br>
   
   VIDEO_US02.mp4

   </details>

3. **[US03] Formatação de Data Amigável ao Usuário (`2026-07-20`)**
   * **O que testar:** Analisar a clareza e o padrão de exibição das datas registradas na tabela de agendamentos.
   * **Comportamento esperado:** As datas devem ser exibidas no formato habitual do Brasil (`DD/MM/AAAA`, ex: `20/07/2026`), tornando a leitura mais natural para a equipe da clínica.
   * **Status:** 🔴 **Reprovado** *(O sistema exibe a data no formato técnico/americano `AAAA-MM-DD`, desacelerando a leitura visual e o entendimento imediato por parte do usuário).*

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (US03)</b></summary>

   <br>
   
   VIDEO_US03.mp4

   </details>

4. **[US04] Destaque Visual para Status da Consulta (`Confirmado` / `Pendente`)**
   * **O que testar:** Avaliar o uso de elementos visuais (como cores e etiquetas) para diferenciar os diferentes estados na coluna **Status**.
   * **Comportamento esperado:** Status diferentes devem ter destaque visual intuitivo (por exemplo, etiqueta verde para "Confirmado" e amarela/laranja para "Pendente"), permitindo bater o olho e entender a situação da agenda.
   * **Status:** 🔴 **Reprovado** *(Os status são exibidos apenas como texto simples em preto, sem diferenciação por cores ou fundo destacado, dificultando a identificação rápida do estado dos agendamentos).*

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (US04)</b></summary>

   <br>
   
   VIDEO_US04.mp4

   </details>

5. **[US05] Sinalização da Seção Ativa no Menu Lateral (`Agendamentos`)**
   * **O que testar:** Verificar se a tela em que o usuário se encontra fica claramente destacada no menu de navegação à esquerda.
   * **Comportamento esperado:** A opção correspondente à página atual deve possuir um contraste visual diferenciado (fundo destacado ou indicador ativo), ajudando o usuário a se orientar no sistema.
   * **Status:** 🟢 **Aprovado** *(O item "Agendamentos" aparece destacado com fundo azul escuro/iluminado no menu lateral, deixando evidente para a recepcionista em qual módulo ela está navegando).*

   <details>
   <summary>📹 <b>Clique para expandir a evidência em vídeo (US05)</b></summary>

   <br>
   
   VIDEO_US05.mp4

   </details>
