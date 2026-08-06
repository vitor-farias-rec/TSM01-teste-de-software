# Atividade Avaliativa: Testes de Performance

> Documento referente à atividade da **Trilha de Testes de Software** na **4ª Edição da Formação Acelerada em Programação (FAP)**.

---

| Informação | Detalhe |
| :--- | :--- |
| **Programa** | FAP 4ª Edição — SOFTEX PE (Coordenação) / Aponti (Execução) |
| **Trilha** | Testes de Software |
| **Módulo / Unidade** | Módulo 01 — Unidade 4 |
| **Sistema Analisado** | Nova versão de Sistema Bancário (Cenário Fictício) |
| **Autor** | Vitor Pontes de Farias ([@vitor-farias-rec](https://github.com/vitor-farias-rec)) |
| **Status** | Em Execução |

---

> **Objetivo da Atividade:**  
> Analisar o sistema para determinar sua aprovação, identificar métricas críticas e gargalos de desempenho, classificar o cenário do teste e propor recomendações técnicas de melhoria à equipe.

---

## O sistema pode ser considerado aprovado?
**Não.** O sistema só pode ser aprovado após a realização dos testes práticos de uso simultâneo. A existência de regras escritas não garante que a tela de entrada e a visualização do saldo funcionarão rápido quando muitos clientes acessarem a conta ao mesmo tempo.

---

## Quais métricas indicam problemas de desempenho?
As principais formas de medir a lentidão ou falha nestes dois fluxos são:

* **Tempo de espera:** A demora para validar a senha na entrada ou a demora para o valor do saldo aparecer na tela.
* **Aumento de falhas e travamentos:** O sistema exibir mensagens de erro inesperadas ou parar de responder quando várias pessoas tentam entrar juntas.
* **Quantidade de atendimentos por segundo:** A queda na quantidade de logins ou consultas de saldo que o sistema consegue concluir a cada segundo.
* **Sobrecarga dos computadores centrais:** O uso exagerado de processamento e memória nos servidores que mantêm o banco funcionando.

---

## Quais possíveis gargalos podem existir?

* **Na Entrada (Login):**
  * **Verificação de segurança muito pesada:** O cálculo feito para conferir a senha é tão complexo que consome todo o processamento do servidor quando vários clientes tentam entrar ao mesmo tempo.
  * **Dificuldade de localização da conta:** O sistema não encontra a conta do cliente rapidamente porque falta uma organização adequada (como um sumário de livro) no banco de dados.
* **No Saldo:**
  * **Cálculos demorados no banco de dados:** O sistema tenta somar e subtrair todas as movimentações passadas do cliente em tempo real, em vez de apenas mostrar o valor final já calculado.
  * **Falta de uma cópia rápida:** O sistema busca as informações na fonte principal toda vez que a tela atualiza, em vez de manter uma cópia temporária do saldo para acesso instantâneo.

---

## Esse cenário se aproxima mais de Carga, Estresse ou Capacidade?
* **Teste de Carga:** Avalia se a entrada e a exibição do saldo funcionam em um tempo aceitável durante um dia normal de movimento no banco.
* **Teste de Estresse:** Força o sistema além do limite (como no dia de pagamento de salários) para descobrir em que momento a tela de entrada ou a consulta de saldo param de funcionar.
* **Teste de Capacidade:** Mede o número exato de pessoas que conseguem verificar o saldo ou fazer o acesso ao mesmo tempo antes do sistema começar a ficar lento.

---

## O que você recomendaria ao time técnico?

1. **Simular acessos simultâneos em ambiente de teste:** Usar programas que imitam centenas de clientes tentando entrar e olhar o saldo ao mesmo tempo antes de liberar o sistema para os usuários reais.
2. **Deixar o saldo pronto para exibição:** Guardar o valor consolidado da conta em um local de fácil acesso para evitar refazer cálculos a cada atualização de tela.
3. **Equilibrar a segurança do acesso:** Ajustar a verificação de senhas para que continue protegida, mas sem exigir esforço excessivo dos computadores do banco.
4. **Criar mecanismos de proteção:** Limitar tentativas excessivas de acesso para evitar que acessos em massa derrubem o sistema.
5. **Acompanhar os indicadores em tempo real:** Usar painéis de visualização durante os testes para identificar e corrigir os pontos de lentidão antes que cheguem ao cliente final.
