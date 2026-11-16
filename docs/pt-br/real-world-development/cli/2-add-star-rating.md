---
title: "Lição 2 - Adicionar avaliações por estrelas: uma vitória rápida"
description: "Use o Copilot CLI para fazer uma pequena alteração nos cards dos jogos, revise-a em um navegador encaminhado e mescle-a como sua primeira pull request."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Agora que você instalou o Copilot CLI e experimentou uma conversa, é hora de fazer sua primeira alteração no projeto. Você manterá isso pequeno: os jogos já têm uma avaliação por estrelas em seus dados, mas os cards dos jogos na página inicial ainda não a exibem. Você pedirá ao agente para revelá-la, revisará a alteração e a mesclará como sua primeira pull request.

Nesta lição, você vai:

- iniciar uma conversa focada do Copilot em uma branch de funcionalidade.
- pedir ao agente que faça uma pequena alteração no projeto.
- revisar a alteração com `/diff`.
- executar o app para confirmar a alteração em um navegador encaminhado.
- abrir e mesclar sua primeira pull request.

## Cenário

Cada jogo da Tailspin Toys pode ter uma avaliação por estrelas, e ela já aparece na página de detalhes do jogo. Os cards dos jogos na página inicial, no entanto, mostram apenas o título, a categoria, o editor e a descrição. Como aquecimento, você fará com que o agente exiba a avaliação existente em cada card — uma mudança pequena e autocontida, perfeita para sua primeira sessão.

## Anatomia de uma conversa

Uma **conversa** é onde você trabalha com o Copilot CLI em uma tarefa. Ao contrário do aplicativo Copilot, uma conversa normal do CLI usa o repositório e o branch do Git atualmente selecionados no seu terminal, em vez de criar uma worktree dedicada. Conversas salvas permitem que você retorne à mesma discussão mais tarde, enquanto os arquivos e o branch continuam sendo estado Git comum no disco.

Dentro de uma conversa, você verá três coisas: suas instruções e as respostas do agente, a atividade de ferramentas do agente enquanto explora e edita arquivos e as alterações que você pode inspecionar com `/diff`.

## Inicie uma conversa e solicite nossa mudança

Vamos começar uma nova conversa para implementar nosso recurso.

1. Volte ao seu Codespace.
2. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Se ainda não estiver aberto, inicie o Copilot com o seguinte comando:

   ```bash
   copilot --yolo
   ```

4. Garanta que uma nova sessão seja iniciada usando o comando de barra `/new` e pressione <kbd>Enter</kbd>.
5. Use o seguinte prompt para solicitar a alteração:

   ```plaintext
   Mostre a starRating de cada jogo em 5 estrelas nos cards na página da lista. Se a avaliação for null, mostre "No rating yet". Mantenha o layout do card como está, adicione testes e execute os checks relevantes.
   ```

O Copilot explora o projeto, localiza os arquivos usados para exibir os detalhes dos jogos e cria o código necessário. Você acabou de adicionar um novo recurso com o Copilot CLI!

## Revisar o diff

Todas as alterações geradas por IA merecem revisão antes de serem mescladas, mesmo pequenas. Vamos explorar as alterações diretamente aqui no Copilot CLI.

1. Digite `/diff` e inspecione cada arquivo alterado.
2. Confirme que o card do jogo exibe a avaliação numérica quando ela está presente e `No rating yet` quando `starRating` é `null`.
3. Confirme que os testes cobrem os dois estados.
4. Revise os resultados dos checks executados pelo Copilot e peça a ele para corrigir qualquer falha.
5. Quando sua revisão estiver concluída, pressione <kbd>Esc</kbd> para sair da tela de diff.

> [!NOTE]
> Como o Copilot, como todas as ferramentas generativas de IA, é probabilístico e não determinístico, seu código exato pode variar. Revise o comportamento em vez de esperar uma implementação exata.

## Verificar as alterações

Claro, não deveríamos apenas ler o código e assumir que ele funciona. Vamos pedir ao Copilot para iniciar nosso site e examinar a interface do usuário atualizada no navegador encaminhado pelos Codespaces.

1. Peça ao Copilot para iniciar o app:

   ```plaintext
   Inicie o app para que eu possa inspecionar a alteração de classificação por estrelas no meu navegador. Me diga a URL e deixe o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Confirme que os cards dos jogos exibem suas avaliações em cinco estrelas.
4. Volte ao Copilot e peça a ele para parar o servidor que iniciou:

   ```plaintext
   Pare o servidor de desenvolvimento que você iniciou.
   ```

## Abrir e mesclar sua primeira pull request

Você agora criou o recurso! É hora de criar uma pull request (PR) para mesclar o novo código no projeto.

1. Peça ao agente padrão para confirmar a alteração:

   ```plaintext
   Confirme as alterações revisadas de classificação por estrelas com uma mensagem de commit apropriada.
   ```

2. Digite `/pr create`. O Copilot CLI envia o commit existente quando cria a PR e mostra a URL da PR.
3. Abra a PR segurando <kbd>Command</kbd> (Mac) ou <kbd>Ctrl</kbd> (Windows/Linux) e selecionando a URL exibida pelo Copilot CLI.
4. Revise os arquivos alterados e os checks.
5. Quando estiver pronto, selecione **Merge pull request** e confirme a mesclagem.
6. Volte ao seu Codespace e saia do Copilot CLI com `/exit`.
7. Atualize seu `main` local:

   ```bash
   git checkout main
   git pull
   ```

## Resumo e próximos passos

Parabéns! Você enviou sua primeira alteração usando o GitHub Copilot CLI! Especificamente, você:

- iniciou uma conversa focada do Copilot em uma branch de funcionalidade.
- orientou o agente a fazer uma pequena alteração nos cards dos jogos.
- revisou a alteração com `/diff`.
- executou o app para confirmar a avaliação por estrelas em um navegador encaminhado.
- abriu e mesclou sua primeira pull request.

Em seguida, você [começará pela issue de filtragem e usará os modos Plan e Autopilot][next-lesson] para criar um recurso maior.

## Recursos

- [Sobre o GitHub Copilot CLI][about-copilot-cli]
- [Referência de comandos do Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
