# Atividade Avaliativa: Plano de Testes

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
> Elaborar um plano de testes de acordo com estratégia pré-definida.

---

## 1. Plano de Testes

### 1.1 Escopo de Testes

| Prioridade | Módulos testados |
|---|---|
| 🔴 Alta | Agendamentos, Reagendamentos, Agenda profissional, Check-in e presença, Salas, Prontuários, Evoluções de sessão, Perfis e permissões |
| 🟠 Média | Dashboard, Recibos, Receitas, Despesas, Relatório financeiro, Pacientes, Psicólogos, Funcionários |
| 🟢 Baixa | Especialidades, Convênios, Produtos e materiais, Controle de estoque |

**Fora deste plano** (pra não prometer mais do que o time e o prazo permitem):
- Testes de invasão/segurança avançada — pediria uma equipe especializada
- Testar em todos os navegadores e celulares existentes — vale combinar antes quais são os mais usados pela clínica
- Simular uma quantidade de acessos muito maior do que uma clínica real teria

### 1.2 Tipos de Teste Aplicados

| Tipo de teste | O que verifica | Como é feito |
|---|---|---|
| Exploratório | Uso livre do sistema, procurando problemas que ninguém pensou em testar | Manual |
| Usabilidade | Se a tela é fácil de entender e usar, incluindo contraste de cores | Manual, com apoio de ferramenta pra medir contraste |
| Smoke (verificação rápida) | Se as funções mais básicas ainda funcionam depois de uma nova versão | Automatizado |
| Sanidade | Se uma correção específica realmente resolveu o problema | Manual |
| Regressão | Se algo que já funcionava parou de funcionar | Automatizado |
| Sistema | O caminho completo de uma tarefa, do início ao fim, passando pelos módulos envolvidos | Começa manual; depois que o fluxo se estabiliza, passa a contar com automação também |
| Desempenho | Se o sistema continua rápido com bastante informação cadastrada | Automatizado |
| Aceitação | Se a equipe da clínica aprova o sistema pra uso real | Manual, feito pela própria equipe da clínica |

### 1.3 Critérios de Entrada e Saída

**Pra começar a testar uma funcionalidade:**
- A tela ou função está pronta e disponível no ambiente de teste
- Nada impede nem abrir a tela (ex: tela em branco, erro ao carregar)
- Existe um mínimo de explicação de como aquilo deveria funcionar

**Pra considerar o teste de uma entrega concluído:**
- Todos os testes planejados foram executados, mesmo que alguns tenham encontrado problema
- Não existe nenhum erro grave em aberto
- Erros médios ou pequenos estão anotados e conhecidos pelo time, mesmo sem solução ainda
- Em entregas grandes, a equipe da clínica já aprovou o fluxo principal no teste de aceitação

Pra classificar a gravidade de um erro:
- **Grave** → impede o uso ou expõe dado de paciente (ex: agendamento duplicado, prontuário visível pra quem não deveria)
- **Médio** → incomoda, mas tem como contornar (ex: contraste ruim numa tela)
- **Pequeno** → detalhe visual ou de texto, sem afetar o uso

### 1.4 Ambiente de Testes

O time já conta com um ambiente de teste separado do sistema real usado pela clínica no dia a dia. Pra ele funcionar bem, o ideal é manter:
- Dados fictícios (pacientes, psicólogos e agendamentos "de mentira"), nunca informação real de paciente
- Os mesmos navegadores e tipo de tela que a equipe da clínica usa de verdade, pra pegar problemas que só aparecem no uso real (como o contraste baixo já encontrado no dashboard)
- Acesso liberado tanto pra quem testa quanto pra quem desenvolve
- Possibilidade de "zerar" os dados de teste e recomeçar quando precisar

### 1.5 Recursos e Responsabilidades

| Quem | Faz o quê |
|---|---|
| Pessoa responsável pelos testes | Planeja os testes, executa o exploratório e o de usabilidade, registra os problemas e confirma se as correções funcionaram |
| Desenvolvedor(es) | Corrige os problemas encontrados, ajuda a manter o ambiente de teste, revisa o próprio trabalho antes de entregar |
| Responsável pela automação | Cria e mantém os testes automáticos de Smoke e Regressão |
| Representante da clínica (recepcionista e/ou psicólogo) | Participa do teste de aceitação, avaliando se o sistema resolve o dia a dia de verdade |
| Responsável pelo projeto | Decide prioridades quando o tempo aperta e aprova se uma entrega pode sair mesmo com algum problema pequeno já conhecido |

Como o time é reduzido, é normal que uma mesma pessoa acumule mais de uma dessas funções — o que importa é que todas fiquem cobertas por alguém.

### 1.6 Cronograma

O prazo de entrega já está definido pelo projeto, então os testes seguem este ritmo, repetindo-se em cada entrega:

| Quando | O que acontece |
|---|---|
| Durante toda a semana | Exploratório e usabilidade em cada funcionalidade nova; smoke a cada versão nova liberada no ambiente de teste |
| Poucos dias antes da entrega | Teste de sistema (fluxo completo) e início da regressão automatizada |
| Véspera da entrega | Regressão completa, checagem das últimas correções e revisão dos erros graves ainda em aberto |
| Fechamento de entregas grandes | Teste de aceitação com a equipe da clínica |
| Depois da entrega | Novo ciclo começa, já considerando o que a equipe da clínica relatar no uso real |

### 1.7 Riscos

| Risco | Impacto | O que fazer |
|---|---|---|
| Prazo curto não permitir testar tudo com o mesmo cuidado | Alto | Seguir a prioridade já definida (Agendamentos e Prontuários primeiro); avisar o time se algo de baixa prioridade ficar de fora |
| Alguém do time pequeno ficar indisponível | Alto | Garantir que pelo menos duas pessoas saibam executar os testes mais importantes |
| Ambiente de teste sair do ar ou dar problema técnico | Alto | Ter uma alternativa simples (testar direto com o desenvolvedor) até o ambiente voltar |
| Uma correção acabar quebrando outra parte do sistema | Médio | Regressão automatizada em toda entrega, pra detectar isso rápido |
| Erro grave aparecer muito perto da entrega | Alto | Ter critério claro de quando adiar a entrega e quando lançar avisando sobre o problema conhecido |
| Dado real de paciente aparecer no ambiente de teste | Muito alto | Garantir que o ambiente de teste use só dados fictícios |
