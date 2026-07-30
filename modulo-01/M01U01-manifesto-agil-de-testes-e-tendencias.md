#  Atividade Avaliativa: Manifesto Ágil de Testes e Tendências

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 1 |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | 🟢 Concluído |

---

## 1. Comparativo: QA Tradicional vs. QA Moderna

| Critério | 🏛️ QA Tradicional |  QA Moderna |
| :--- | :--- | :--- |
| **Definição & Conceito** | Conjunto de práticas de teste realizadas ao **final do ciclo de desenvolvimento**, após a implementação. Executado por uma equipe de QA isolada do time de dev, seguindo um processo sequencial de planejamento, execução e registro de bugs. | Conjunto de práticas em que a qualidade é **responsabilidade de todo o time**, presente em todas as etapas. Inclui *Agile Testing* (sprints com feedback contínuo), *Automação*, *Shift Left* (testes antecipados) e *DevSecTestOps* (segurança e testes integrados ao pipeline de CI/CD). |
| **Vantagens** | • Processo estruturado com planos e casos de teste bem documentados.<br>• Papéis e responsabilidades bem delimitados.<br>• Adequado para projetos com requisitos estáveis e pouca mudança de escopo. | • **Detecção antecipada de defeitos**, reduzindo custo e tempo de correção.<br>• Feedback rápido e contínuo para os desenvolvedores.<br>• Alta cobertura de testes de regressão via automação.<br>• Entregas mais rápidas, seguras e frequentes. |
| **Limitações** | • Defeitos encontrados tardiamente (alto custo de retrabalho).<br>• Processo lento devido a testes majoritariamente manuais.<br>• Dificuldade para acompanhar ritmos ágeis e entregas frequentes. | • Exige investimento inicial em ferramentas e capacitação técnica.<br>• Nem tudo pode ser automatizado (ex: testes exploratórios e de usabilidade ainda exigem intervenção humana). |

>  **Highlight:** A evolução para a **QA Moderna** reposiciona o testador de uma função puramente operacional para um papel estratégico, focado na prevenção contínua de falhas em todo o fluxo de entrega.

---

## 2. Quais desafios atuais de QA mais impactam projetos reais?

A transição para ecossistemas ágeis e de entrega contínua trouxe novos obstáculos para a garantia da qualidade no dia a dia dos times de tecnologia. Os três principais desafios identificados são:

###  1. Equilíbrio entre Velocidade e Profundidade
* Sprints curtas e pipelines de **CI/CD com múltiplos deploys diários** reduzem drasticamente a janela de tempo disponível para validações completas.
* A pressão por lançamentos rápidos frequentemente resulta no vazamento de falhas para o ambiente de produção.

###  2. Lacuna de Competências (*Skills Gap*)
* O perfil do profissional de QA tornou-se multidisciplinar: exige-se escrita e manutenção de código para automação, compreensão de esteiras de CI/CD e conhecimentos de **segurança (DevSecTestOps)**.
* Essa combinação de habilidades avançadas ainda é escassa no mercado, exigindo constante capacitação das equipes.

###  3. Complexidade Arquitetural dos Sistemas
* A predominância de arquiteturas baseadas em **microsserviços, integrações via API e ambientes multicloud** torna extremamente complexo reproduzir e isolar cenários reais de teste.

>  **Conclusão:** Enfrentar esses desafios exige a consolidação da cultura de qualidade compartilhada, investimento em automação de testes e aprendizado técnico contínuo.
