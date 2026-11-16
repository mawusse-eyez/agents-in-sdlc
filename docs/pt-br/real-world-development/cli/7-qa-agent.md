---
title: "Lição 7 - Criar e usar um agente de QA"
description: "Crie um agente personalizado de QA que combine requisitos de issue, a skill quality-checks e o Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Você já usou a skill `quality-checks` para executar verificações automatizadas e o Playwright MCP para observar a experiência de filtragem em um navegador. Agora você vai unir essas capacidades em um agente personalizado com um processo de QA claramente definido.

Nesta lição, você vai:

- explorar como um agente personalizado trabalha com instruções, skills e ferramentas MCP.
- criar e inspecionar um perfil reutilizável de garantia de qualidade.
- selecionar o agente de QA e revisar suas descobertas em relação à issue de filtragem.

## Cenário

A Tailspin Toys quer uma revisão consistente de requisitos, qualidade de código, verificações automatizadas, cobertura de testes e comportamento do navegador antes de abrir uma pull request (PR). Um agente personalizado pode coordenar esse processo de QA e fornecer um relatório reutilizável.

## O que é um agente personalizado?

Um agente personalizado é uma versão especializada do Copilot definida em um perfil Markdown. O perfil descreve o objetivo do agente, as instruções e as ferramentas disponíveis. Para este workshop, você definirá uma função de QA em `.github/agents/qa.agent.md` e a selecionará no Copilot CLI.

As customizações que você usou têm trabalhos diferentes. As instruções do repositório descrevem os padrões da equipe. A skill `quality-checks` empacota verificações repetíveis. O Playwright MCP fornece ferramentas de navegador. O perfil de QA diz ao Copilot como usar essas capacidades para avaliar requisitos e relatar descobertas. Ele não substitui essas ferramentas nem exige outra conversa.

## Criar o perfil de QA

Antes de abrir a PR do recurso, você pedirá ao Copilot para criar um perfil de QA reutilizável. O perfil definirá tanto as verificações que a QA executa quanto os limites que ela deve seguir.

1. Volte ao seu Codespace e confirme que a conversa de filtragem está no modo Interativo.
2. Peça ao agente padrão para criar o novo agente personalizado:

   ```plaintext
   Crie um agente personalizado chamado QA em .github/agents/qa.agent.md. Ele deve verificar recursos em relação às issues e aos requisitos acordados, seguir as instruções do repositório, executar a skill quality-checks, usar o Playwright MCP para verificar o comportamento e adicionar testes quando a cobertura estiver ausente.

   Faça com que ele relate cada requisito como aprovado, falhou ou bloqueado, com evidências de suporte. Ele deve pedir antes de alterar o código de implementação e não deve confirmar alterações nem abrir pull requests.

   Apenas crie o perfil por enquanto para que eu possa revisá-lo.
   ```

## Inspecionar o perfil

Antes de usar o novo agente, revise o perfil para confirmar que o Copilot capturou o fluxo de trabalho de QA e os limites pretendidos. Isso evita que um agente incompleto ou excessivamente amplo altere o recurso quando você só quer verificá-lo.

1. Digite `/diff` e abra `.github/agents/qa.agent.md`.
2. Leia o frontmatter. A `description` é obrigatória; `name` é opcional, mas incluí-la fornece ao agente um nome de exibição claro.
3. Leia as instruções do perfil e confirme que a QA começa a partir dos requisitos, segue as instruções do repositório, executa a skill `quality-checks` e usa o Playwright MCP.
4. Confirme que a QA relata evidências de suporte, pede antes de alterar o código de implementação e não confirma alterações nem abre pull requests.
5. Se o perfil gerado deixar de cobrir alguma dessas responsabilidades ou limites, peça ao agente padrão para revisá-lo antes de continuar.

## Executar a QA contra a issue

O Copilot CLI carrega os agentes do projeto quando uma conversa começa. Retome a mesma conversa de filtragem depois de criar o perfil e selecione QA para que ele possa usar a issue e as decisões de planejamento já em contexto.

1. Ative o agente usando o seguinte prompt:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como você acabou de criar o agente, ele pode não aparecer na lista de agentes disponíveis. Ele está lá e o comando acima o ativará.

2. Use o seguinte prompt para pedir ao agente de QA que revise o recurso:

   ```plaintext
   Revise o recurso de filtragem em relação à issue e às decisões do nosso plano. Ele está pronto para uma PR?
   ```

3. O agente de QA começa a trabalhar!
4. Leia o relatório que ele fornece quando terminar o trabalho!

## Resumo e próximos passos

Você adicionou um papel especialista reutilizável ao fluxo de trabalho e revisou o trabalho. Nesta lição, você:

- explorou como um agente personalizado funciona com instruções, skills e ferramentas MCP.
- criou e inspecionou um perfil reutilizável de garantia de qualidade.
- selecionou o agente de QA e revisou suas descobertas em relação à issue de filtragem.

Agora você já tem a implementação, a atualização da skill, o perfil de QA, os testes e o relatório de verificação prontos para revisão. Em seguida, você [vai reuni-los em uma PR de recurso e usar o Agent Merge][next-lesson].

## Recursos

- [Criar agentes personalizados para o Copilot CLI][create-agents]
- [Configuração de agente personalizado][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
