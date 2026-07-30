# Atividade Avaliativa: Metodologias de Desenvolvimento — Ágil vs. Cascata

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 2 |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Concluído |

---

> **Objetivo da Atividade:**  
> Produzir uma tabela comparativa entre as metodologias Ágil e Cascata, indicando como os testes acontecem em cada modelo, além de suas respectivas vantagens e limitações.

---

## Tabela Comparativa: Ágil vs. Cascata

| Critério | Metodologia Ágil | Metodologia Cascata |
| :--- | :--- | :--- |
| **Definição e Conceito** | Baseada em ciclos iterativos e incrementais, tendo o formato Scrum de 2 semanas para cada entrega como o modelo mais clássico. | Orientada por um modelo linear composto por uma sequência de etapas: Requisitos, Design, Implementação, Verificação e Manutenção. |
| **Como os Testes Acontecem** | Ocorrem de forma **contínua e integrada** a cada sprint. Testam-se pequenos incrementos funcionais em paralelo ao desenvolvimento, gerando feedback rápido e identificação precoce de falhas. | Ocorrem em uma **fase única e tardia** (etapa de Verificação), realizada exclusivamente após a conclusão de toda a fase de implementação e codificação do sistema. |
| **Vantagens** | • Abordagem adaptativa com menor retrabalho e custos enxutos.<br>• Defeitos no código são evidenciados continuamente.<br>• Permite integração contínua com partes do código funcionais e independentes. | • Estrutura de gerenciamento sequencial bem definida, facilitando a organização.<br>• Documentação robusta, proporcionando maior rastreabilidade e clareza de papéis. |
| **Limitações** | • Documentação menos robusta, dificultando a estimativa precisa de custos e prazos longos. | • Estrutura rígida com pouca adaptação a mudanças e pouca participação do cliente.<br>• Erros e retrabalhos são identificados no final, gerando custos elevados de correção. |

---

## Resumo dos Impactos na Garantia da Qualidade

### Modelo Ágil
* **Testagem Contínua:** A validação acontece durante todo o ciclo de vida da sprint, reduzindo o custo de correção e evitando o acúmulo de bugs para a entrega final.
* **Foco na Mudança:** Permite redefinir critérios de teste conforme as necessidades do cliente e do negócio evoluem.

---

### Modelo Cascata
* **Testagem em Bloco:** A fase de testes só começa quando a codificação termina. Se os requisitos iniciais estiverem incorretos, todo o código precisará ser reescrito.
* **Documentação Base:** Os testes são executados estritamente com base na documentação e nos casos de teste planejados na fase inicial de Requisitos.
