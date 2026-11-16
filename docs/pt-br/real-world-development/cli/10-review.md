---
title: "Lição 10 - Encerramento e próximos passos"
description: "Revise o fluxo de trabalho do Copilot CLI, duas pull requests, customizações reutilizáveis e recursos adicionais."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Você usou o GitHub Copilot CLI em um fluxo contínuo de trabalho da Tailspin Toys. Você:

- preparou um Codespace, instalou o Copilot CLI, explorou o projeto e encontrou a issue de filtragem inicial.
- adicionou avaliações por estrelas, revisou o resultado em um navegador encaminhado e mesclou manualmente sua primeira pull request (PR).
- começou pela issue de filtragem, definiu a abordagem no modo Plan, construiu no modo Autopilot e revisou no modo Interativo.
- guiou o agente com instruções personalizadas, depois personalizou a skill existente `quality-checks` e usou-a para executar testes unitários, lint e verificações de tipo.
- adicionou o servidor Model Context Protocol (MCP) do Playwright e usou-o para explorar a filtragem em um navegador real.
- criou e selecionou um agente personalizado de garantia de qualidade (QA) para avaliar requisitos, cobertura, resultados da skill e evidências do navegador.
- revisou a alteração completa de filtragem e autorizou o Agent Merge para a PR de filtragem.
- explorou comandos de barra para contexto, modelos, compartilhamento e delegação opcional para a nuvem.

## O que você entregou

O workshop tem dois marcos de PR, cada um em uma branch separada a partir do `main` atualizado:

1. **Avaliações por estrelas:** exibe a `starRating` existente e um estado explícito de não avaliado nos cards de jogos.
2. **Filtragem e fluxo de qualidade:** implementa a filtragem, atualiza as instruções e as aplica ao recurso, personaliza o relatório `quality-checks`, cria um perfil de QA e inclui os testes associados.

Da análise de planejamento da filtragem até a abertura da PR, você usou a mesma conversa e branch. Combinamos esse trabalho em uma única PR para simplificar o workshop.

## Tipos diferentes de verificação

Você verificou o código de várias maneiras: testes automatizados, sua própria inspeção do navegador e a exploração do navegador do Copilot por meio do MCP. A skill `quality-checks` executou testes unitários, lint e verificações de tipo e relatou os resultados em seu novo formato. O QA reuniu esses resultados com uma revisão de requisitos e cobertura de testes antes da PR.

Os testes adicionados devem fechar lacunas reais; uma execução de QA que não precise de novos testes pode estar correta. Revise o código e as evidências antes de autorizar a mesclagem e atualize as evidências afetadas após alterações.

## Melhores práticas

O contexto e as ferramentas que você fornece ao Copilot moldam seu trabalho. Neste workshop, você atualizou instruções, personalizou uma skill, criou um perfil de QA e configurou um servidor MCP. Reaproveite essas customizações em diferentes conversas e ajuste-as conforme as necessidades da sua equipe. As instruções definem padrões, as skills descrevem tarefas repetíveis, os agentes personalizados definem papéis especializados e os servidores MCP conectam ferramentas externas. Revise as alterações reais e os resultados das ferramentas, não apenas o resumo do agente.

Combine o **modo e o modelo** com a tarefa. Use **Plan** para pensar na abordagem antes de construir, **Interactive** para ficar no controle em alterações focadas e **Autopilot** para tarefas bem delimitadas. Escolha um modelo mais rápido para edições de rotina e um mais capaz para trabalhos complexos.

O contexto continua sendo tão importante quanto a infraestrutura. Descrever claramente *o que* você quer construir, *por quê* e *como* muda significativamente a saída.

## Mais para explorar

Você cobriu o fluxo principal. Alguns recursos adicionais do CLI que valem a pena conhecer:

- `/review` para pedir ao agente de revisão de código que analise as alterações.
- `/rubber-duck` para discutir um problema e obter outra perspectiva.
- `/fleet` para orquestrar subtarefas independentes em paralelo.
- `/worktree` para isolar uma tarefa separada.
- `/delegate` para enviar uma tarefa ao agente de nuvem do Copilot.

## Próximos passos

A melhor maneira de melhorar com qualquer ferramenta é continuar usando-a! Use-a para código de produção, para código pessoal, para o pequeno aplicativo que você sempre quis criar, mas nunca teve tempo. Compartilhe seus aprendizados com a equipe e aprenda com os deles. E, como sempre, explore a documentação.

Se você quiser estender a Tailspin Toys pelo terminal, continue com a série opcional [Foundry Backer Concierge][foundry]. Para comparar outros ambientes, explore o [workshop do VS Code][vscode], o [workshop do aplicativo GitHub Copilot][app] ou o [workshop do agente de nuvem do GitHub Copilot][cloud].

## Recursos

- [Sobre o GitHub Copilot CLI][about-cli]
- [Referência de comandos do Copilot CLI][cli-reference]
- [Personalizar o Copilot CLI][customize-cli]
- [Gerenciar pull requests com o Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
