---
title: "Lição 6 - Validar a funcionalidade com o Playwright MCP"
description: "Inspecione ou configure o Playwright MCP no Copilot CLI e use-o para explorar a funcionalidade de filtragem em um navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como já destacamos, escrever código não é apenas escrever código. Precisamos trabalhar com dados, serviços externos e até permitir automações adicionais para o Copilot. É aí que os servidores MCP entram em cena. Os servidores MCP permitem que o Copilot vá além do que já está integrado ao CLI, fornecendo mais ferramentas e serviços.

Nesta lição, você vai:

- entender o que é Model Context Protocol (MCP) e como o Copilot CLI o usa.
- adicionar o servidor Playwright MCP se ele ainda não estiver disponível.
- pedir ao agente para conduzir um navegador e explorar sua funcionalidade de filtragem.

## Cenário

Embora testes unitários e end-to-end sejam importantes, validar atualizações na interface do usuário exige interagir de fato com a interface. Você quer permitir que o Copilot use o site em que está trabalhando como um usuário faria para automatizar ainda mais como as alterações são feitas, fornecendo mais confiança de que as atualizações funcionam como esperado.

## O que é Model Context Protocol (MCP)?

[Model Context Protocol (MCP)][mcp-blog-post] oferece aos agentes de IA uma maneira de se comunicar com ferramentas e serviços externos. Ao usar o MCP, agentes de IA podem se comunicar com ferramentas e serviços externos em tempo real. Isso permite acessar informações atualizadas e executar ações em seu nome.

Essas ferramentas e recursos são acessados por meio de um servidor MCP, que atua como ponte entre o agente de IA e as ferramentas e serviços externos. Cada servidor MCP representa um conjunto diferente de ferramentas e recursos que o agente de IA pode acessar.

Alguns servidores MCP populares são:

- **[GitHub MCP Server][github-mcp]**: fornece acesso a APIs para gerenciar repositórios, issues e pull requests do GitHub.
- **[Playwright MCP Server][playwright-mcp-server]**: fornece capacidades de automação de navegador usando o Playwright.

Há muitos outros servidores MCP disponíveis. O GitHub hospeda um [registro MCP][mcp-registry] para aumentar a descoberta e as contribuições ao ecossistema.

> [!CAUTION]
> Trate os servidores MCP como faria com qualquer outra dependência do seu projeto. Antes de usá-lo, revise o código-fonte, verifique o editor e considere as implicações de segurança.

## Adicionar o servidor Playwright MCP

Se o servidor Playwright MCP ainda não estiver disponível, adicione-o para que o Copilot possa interagir com o site como um usuário faria.

> [!NOTE]
> Se o Playwright MCP já estiver configurado no Copilot CLI, ignore estes passos de configuração e continue para a próxima seção.

1. Volte ao seu Codespace.
2. Abra a caixa de diálogo para adicionar um servidor MCP digitando o seguinte comando no Copilot CLI:

   ```plaintext
   /mcp add
   ```

3. Para o nome, digite `playwright` e pressione <kbd>Tab</kbd>.
4. Confirme um tipo de servidor **STDIO** pressionando <kbd>Enter</kbd> e em seguida <kbd>Tab</kbd>.
5. Cole o seguinte no diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pressione <kbd>Control</kbd>+<kbd>S</kbd> (Mac) ou <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para salvar o novo servidor MCP.
7. Pressione <kbd>Esc</kbd> para sair da caixa de diálogo do MCP.

## Pedir ao Copilot para explorar o recurso via Playwright

Anteriormente, você confirmou manualmente que a funcionalidade funciona como esperado. Agora vamos usar o servidor Playwright MCP disponível no Copilot para fazer o mesmo!

1. Use o seguinte prompt para dizer ao Copilot para usar o servidor Playwright MCP para validar a funcionalidade:

   ```plaintext
   Inicie o app e use o Playwright MCP para verificar a filtragem com base na issue e no nosso plano. Me diga o que funciona e o que não funciona, sem fazer alterações. Pare o servidor que você iniciou quando terminar.
   ```

> [!NOTE]
> Você não precisa dizer explicitamente ao Copilot para usar o servidor MCP, porque ele normalmente consegue descobrir isso sozinho. Mas como você sabe o que ele deve usar, nunca é uma má ideia apontar na direção certa! Isso ajuda a garantir resultados mais consistentes e economiza alguns tokens.

2. Observe enquanto o Copilot lista as várias etapas que executa no navegador para confirmar que a funcionalidade funciona.
3. Leia o relatório e garanta que tudo esteja funcionando como esperado.

O Copilot iniciará o servidor, usará o Playwright para interagir com o site, terminará o servidor e fornecerá um relatório.

## Resumo e próximos passos

Parabéns, você usou o servidor Playwright MCP para explorar seu recurso em um navegador real a partir do Copilot CLI! Para recapitular, você:

- aprendeu o que é Model Context Protocol (MCP) e como o Copilot CLI o usa.
- adicionou o servidor Playwright MCP se ele ainda não estivesse disponível.
- pediu ao agente para conduzir um navegador e explorar a funcionalidade de filtragem.

Em seguida, você [criará um agente personalizado de QA][next-lesson] que reúne a skill e as ferramentas do navegador em um papel especialista.

## Recursos

- [O que diabos é MCP e por que todo mundo está falando sobre isso?][mcp-blog-post]
- [Servidor Playwright MCP da Microsoft][playwright-mcp-server]
- [Adicionar servidores MCP ao Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
