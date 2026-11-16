---
title: "Lição 8 - Criar e mesclar a PR do recurso"
description: "Revise a filtragem, instruções, atualização da skill, perfil de QA e testes juntos, depois crie uma PR e use o Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Sua implementação de filtragem, atualizações de instruções, atualização da skill, perfil de garantia de qualidade (QA) e testes estão salvos em uma branch. É hora de revisá-los juntos e abrir uma pull request. Você mesclou a pull request de avaliação por estrelas por conta própria; desta vez você permitirá que o **Agent Merge** gerencie o processo.

> [!NOTE]
> Normalmente, dividiríamos o recurso, as atualizações de instruções, a atualização da skill e o agente de QA em algumas PRs separadas. Para simplificar o workshop, você manteve todo o fluxo de filtragem e qualidade em uma conversa e branch, com todo esse trabalho indo para esta PR.

Nesta lição, você vai:

- aprender o que é Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionar a mudança completa do recurso e as evidências de verificação.
- criar a PR de filtragem.
- habilitar o Agent Merge somente após a revisão e confirmar que a PR foi mesclada.

## Cenário

Ao longo do fluxo de filtragem, você usou o Copilot para planejar, implementar e verificar um recurso. A Tailspin Toys agora deseja automatizar o restante do trabalho de PR, mantendo a autorização de mesclagem sob o controle do desenvolvedor.

## Apresentando o Agent Merge

**Agent Merge** automatiza o trabalho restante necessário para incluir uma pull request. Quando você o habilita, o Copilot trabalha no que bloqueia a PR — corrigindo checks falhando de integração contínua (CI), respondendo a comentários de revisão e rebase quando necessário — e então habilita o auto-merge do GitHub quando o repositório permitir.

Até este ponto, você selecionou **Merge pull request** por conta própria. O Agent Merge pode assumir essa responsabilidade. Revise o trabalho e decida se ele está pronto antes de habilitar o Agent Merge.

## Usar o Agent Merge para gerenciar a PR

Com todo o seu código criado, vamos revisá-lo juntos, criar a PR e permitir que o Agent Merge gerencie o restante do processo.

1. Volte ao seu Codespace.
2. Abra a caixa de diálogo do agente digitando `/agent`.
3. Selecione **Default** na lista de opções e pressione <kbd>Enter</kbd>.
4. Crie uma nova PR usando o comando `/pr create`.
5. Ative o merge do agente usando `/pr agentmerge`.
6. O Copilot observará o processo de integração contínua na PR. Quando tudo for bem-sucedido, ele executará a mesclagem.
7. Certifique-se de ver uma mensagem do Copilot parecida com "PR #14 foi squash-merged successfully."

> [!IMPORTANT]
> O Agent Merge não contorna aprovações obrigatórias, proteção de branch, filas de merge, configurações do repositório ou permissões ausentes. Se ele for bloqueado, leia a razão informada e conclua a mesclagem revisada manualmente quando o seu repositório permitir.

## Resumo e próximos passos

Você automatizou várias partes do processo de desenvolvimento, incluindo geração de código, teste e validação de código e, agora, o processo de pull request. Você:

- aprendeu o que é Agent Merge e como ele automatiza o ciclo de vida da mesclagem.
- inspecionou a mudança completa do recurso e as evidências de verificação.
- criou a PR de filtragem.
- habilitou o Agent Merge somente após a revisão e confirmou que a PR foi mesclada.

Em seguida, você [explorará mais comandos úteis de barra do Copilot CLI][next-lesson] para contexto, modelos, compartilhamento e delegação opcional à nuvem.

## Recursos

- [Gerenciar pull requests com o Copilot CLI][manage-prs]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
