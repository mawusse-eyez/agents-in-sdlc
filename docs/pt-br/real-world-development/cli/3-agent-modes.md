---
title: "Lição 3 - Modos de agente: Plan e Autopilot"
description: "Use o Plan para concordar com uma abordagem, o Autopilot para construir a filtragem a partir de uma issue e o modo Interativo para revisar o resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Começamos adicionando um pequeno recurso ao nosso projeto. Mas alterações maiores exigem um processo mais robusto. Felizmente, o GitHub Copilot CLI foi criado para funcionar com o fluxo existente da organização, garantindo que construamos as coisas certas da maneira certa. Esta é a primeira de várias lições em que você seguirá um processo típico de desenvolvimento guiado por agente, começando usando uma issue para gerar um novo recurso, garantindo que o código seja válido, o recurso funcione como esperado e, eventualmente, seja integrado com sucesso ao projeto.

> [!NOTE]
> Você usará a mesma conversa e branch conforme continuar pelo fluxo do recurso. Normalmente, você teria branches ou PRs diferentes para os diferentes tipos de arquivo com os quais trabalharia, mas vamos usar um atalho para nos ajudar a focar nos conceitos centrais.

Para começar, nesta lição, você vai:

- iniciar uma nova conversa do Copilot a partir de uma issue do GitHub.
- definir requisitos no modo Plan.
- implementar o novo recurso usando o modo Autopilot.
- revisar o código.
- validar o recurso manualmente em um navegador encaminhado.

À medida que você continua nesta funcionalidade, você atualizará as instruções do repositório, personalizará a skill existente `quality-checks`, adicionará validação com MCP, criará um agente de QA e abrirá a PR do recurso.

## Cenário

O catálogo da Tailspin Toys está crescendo, e os visitantes precisam reduzir os jogos por categoria e editor. A issue do backlog descreve o recurso, mas detalhes como combinar categorias precisam ser acordados antes da codificação. Você usará o modo Plan para resolver essas decisões e, em seguida, autorizará uma implementação limitada com o Autopilot.

## Contexto

Introduzir agentes de codificação de IA ao seu fluxo de desenvolvimento não muda os fundamentos. Se alguma coisa, eles se tornam ainda mais importantes! A maioria dos desenvolvedores segue um fluxo semelhante a:

1. Começar a partir de uma issue registrada que descreve o que precisa ser feito.
2. Criar um plano do que precisa ser construído.
3. Construir e revisar o código.
4. Executar os testes para validar o código.
5. Validar manualmente a nova funcionalidade.
6. Criar uma pull request (PR).
7. Depois que o código foi revisado e o processo de integração contínua foi bem-sucedido, mesclar o código.

> [!NOTE]
> Dependendo da sua equipe e organização, os detalhes exatos podem variar. Mas a maioria será uma variação do tema listado acima.

Ao seguir esta abordagem padrão, você garante que o código gerado por IA atenda aos requisitos definidos e passe pelo mesmo processo de validação que o código escrito manualmente.

## Modos de conversa

O **modo de conversa** controla quanta autonomia o agente tem. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar entre os modos:

- **Interactive**: Você e o agente trabalham juntos. O agente sugere alterações e espera sua entrada antes de continuar.
- **Plan**: O agente cria um plano primeiro e é bloqueado para editar arquivos do projeto.
- **Autopilot**: O agente trabalha de forma autônoma — escrevendo código, executando testes e iterando até que a tarefa seja concluída.

Comece no modo Plan, revise o plano e use o Autopilot para implementar.

## Começar pela issue

Antes de iniciar o trabalho de filtragem, volte ao seu Codespace e certifique-se de que o repositório e o terminal estejam prontos.

1. Volte ao seu Codespace. Se estiver parado, reinicie-o antes de continuar.
2. Confirme que a PR de avaliação por estrelas foi mesclada.
3. Se o terminal não estiver aberto, pressione <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Atualize o `main` e depois crie uma branch para o trabalho de filtragem:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicie o Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pressione <kbd>Tab</kbd> duas vezes para abrir a aba **Issues**.
7. Pressione <kbd>A</kbd> para mostrar todas as issues.
8. Use as setas para destacar a issue intitulada **Allow users to filter games by category and publisher**.
9. Pressione <kbd>C</kbd> para adicionar a issue ao prompt e retornar à aba **Session**.

Observe como o prompt agora começa com `#7` (ou um número parecido). O `#` permite trazer uma issue ou pull request (PR) do GitHub para o contexto.

## Planejar o recurso de filtragem

Planejar dá a você a chance de definir a abordagem a ser tomada para implementar um recurso ou realizar tarefas antes de entregar ao Copilot. É sempre uma boa ideia gastar um pouco de tempo planejando qualquer tarefa complexa. Vamos mudar para o modo plan e pedir ao Copilot para criar o plano.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para alternar para o modo Plan. Confirme que o indicador do modo abaixo do prompt mostra **Plan**.
2. Depois da referência da issue adicionada no passo anterior, digite o seguinte prompt:

   ```plaintext
   Crie um plano para implementar este recurso.
   ```

O Copilot começa a trabalhar na construção do plano. Ele vai explorar o projeto e em seguida determinar a melhor abordagem.

3. Ao longo do caminho, o Copilot pode fazer perguntas sobre como as capacidades de filtragem devem funcionar. Responda com base nas suas preferências. Não há respostas erradas aqui!
4. Quando o plano estiver concluído, pressione <kbd>Control</kbd>+<kbd>E</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para expandir o plano.
5. Role para cima e para baixo para revisar o plano.
6. Peça ao Copilot para revisar qualquer parte do plano que não corresponda às suas decisões.

## Aprovar o Autopilot

Com o plano escrito e revisado, é hora de implementá-lo! Vamos deixar o Copilot fazer o trabalho usando o autopilot.

O Autopilot permite que o Copilot itere sobre o problema até acreditar que ele está concluído.

1. Selecione **Accept plan and build on autopilot (recommended)**, ou a opção de rótulo semelhante na sua versão instalada.
2. Confirme que o indicador do modo abaixo do prompt mostra **Autopilot**.
3. Observe enquanto o Copilot itera sobre o plano estabelecido, gera código e executa testes.

> [!NOTE]
> A aprovação pode iniciar a implementação imediatamente, então revise o plano primeiro. Se o Copilot relatar dependências ausentes ou conflito de porta, resolva o problema de configuração antes de tratar os checks como concluídos.

## Revisar e verificar a implementação

Quando o código é gerado, ele precisa ser revisado antes de ser mesclado, como qualquer outro código. Vamos revisar o código e executar o site para garantir que tudo esteja bom.

1. Pressione <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar no modo Interativo. Confirme que o indicador do modo não mostra mais **Plan** ou **Autopilot**.
2. Digite `/diff` e inspecione a implementação de filtragem e os testes.
3. Compare o resultado com a issue e as decisões que você tomou durante o planejamento.
4. Quando o código for revisado, pressione <kbd>Esc</kbd> para sair da visualização diff.
5. Revise a saída dos checks do projeto e peça ao Copilot para resolver qualquer falha.

## Explorar a nova funcionalidade

OK, o código está bom — mas ele funciona? Vamos iniciar o app como antes e abrir o site pelo porto encaminhado do Codespaces.

1. Peça ao Copilot para iniciar o app:

   ```plaintext
   Inicie o app para que eu possa testar a funcionalidade de filtragem no meu navegador. Me diga a URL e deixe o servidor em execução.
   ```

2. Quando o Codespaces informar que a porta `4321` está disponível, selecione **Open in Browser**.
3. Tente a filtragem por categoria, por editor e pelas combinações acordadas no plano.
4. Confirme que o comportamento de reset e de resultado vazio combinem com a issue e suas decisões.
5. Volte ao seu Codespace e peça ao Copilot para parar o servidor de desenvolvimento que iniciou.

## Resumo e próximos passos

Você usou diferentes modos de conversa para construir e revisar um recurso. Nesta lição, você:

- iniciou uma nova conversa do Copilot a partir de uma issue.
- definiu requisitos no modo Plan.
- implementou o novo recurso usando o modo Autopilot.
- revisou o código.
- validou a funcionalidade manualmente em um navegador encaminhado.

Em seguida, vamos aprofundar um pouco mais em como o código é gerado, garantindo que ele siga práticas documentadas, usando [instruções personalizadas][next-lesson].

## Recursos

- [Autopilot no GitHub Copilot CLI][autopilot]
- [Referência de comandos do Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
