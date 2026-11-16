---
title: "Lição 4 - Guiando o Copilot com instruções personalizadas"
description: "Explore instruções do repositório, adicione um padrão de documentação e aplique-o ao código de filtragem."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

O contexto é fundamental ao trabalhar com IA generativa. Se uma tarefa precisar ser feita de uma maneira específica, você quer que essa orientação esteja disponível para o Copilot. [Arquivos de instrução][instruction-files] descrevem não apenas *o que* você quer de código, mas *como* ele deve ser estruturado. Agora que você criou a filtragem, vai explorar as instruções que o Copilot usou, adicionar um padrão de documentação e aplicá-lo ao seu código.

Nesta lição, você vai:

- explorar como instruções do repositório e arquivos de instrução com escopo por caminho chegam ao agente.
- atualizar o arquivo de instruções para garantir que os padrões de codificação sejam seguidos.
- ver o impacto dos arquivos de instrução no código.

## Cenário

Como qualquer boa empresa de desenvolvimento, a Tailspin Toys tem um conjunto de diretrizes e requisitos para práticas de desenvolvimento. Esses incluem:

- Comentários devem explicar a intenção e decisões não óbvias, em vez de repetir o código.
- Funções exportadas em `db/` e `src/lib/` devem documentar sua finalidade, parâmetros e valores de retorno com TSDoc/JSDoc, incluindo um argumento `db` injetável quando presente.
- Componentes Astro reutilizáveis devem documentar seu contrato de `Props`, e os comentários devem permanecer atualizados quando o código relacionado mudar.
- A formatação e a orientação de lint existentes devem ser preservadas.

Por meio do uso de arquivos de instrução, você garantirá que o Copilot tenha as informações corretas para executar as tarefas em alinhamento com as práticas destacadas.

## Arquivos de instrução

Instruções personalizadas permitem fornecer contexto e preferências ao Copilot para que ele entenda melhor seu estilo de programação e seus requisitos. Esse é um recurso poderoso para orientar o Copilot a obter sugestões e trechos de código mais relevantes. Você pode especificar suas convenções de programação preferidas, bibliotecas e até os tipos de comentários que gosta de incluir em seu código. Você pode criar instruções para todo o repositório ou para tipos específicos de arquivos para contexto no nível da tarefa.

Há dois tipos de arquivos de instrução:

- `.github/copilot-instructions.md`, um único arquivo de instrução enviado ao Copilot para **toda** solicitação do repositório. Este arquivo deve conter informações relevantes ao nível do projeto.
- Arquivos `.github/instructions/*.instructions.md`, que fornecem diretrizes para linguagens, tipos de arquivo ou tarefas específicas.

> [!NOTE]
> Outros formatos e suporte de instruções variam de acordo com o ambiente. Consulte a [referência de suporte para instruções personalizadas][custom-instructions-support] antes de depender de um formato específico.

## Explorar os arquivos de instruções personalizadas deste projeto

Para começar, um conjunto de arquivos de instrução já foi incluído com o projeto inicial. Vamos explorá-los antes de fazer uma alteração para ver o impacto.

1. Volte ao seu Codespace.
2. No editor do Codespaces (e não no terminal), abra `.github/copilot-instructions.md`.
3. Explore o arquivo, observando a breve descrição do projeto e suas orientações de codificação. Essas instruções se aplicam a qualquer interação com o Copilot neste repositório.
4. Abra a pasta `.github/instructions` e explore os arquivos. Observe que há instruções para arquivos Astro, a camada de dados Drizzle, testes e muito mais.
5. Abra `.github/instructions/unit-tests.instructions.md`. Observe o campo `applyTo` no topo — isso define um glob que determina a quais arquivos as instruções se aplicam.
6. Abra `.github/instructions/drizzle.instructions.md` e observe seus links para outras instruções e arquivos existentes do projeto. Isso permite quebrar conjuntos maiores de instruções em arquivos menores e reutilizáveis e apontar o Copilot para exemplos a seguir.

## Atualizar os arquivos de instrução para combinar com a orientação da equipe

Embora os arquivos já criados sejam um bom começo, ainda há uma lacuna. Vamos modificar o arquivo central `copilot-instructions.md` para garantir que comentários TSDoc sejam adicionados ao TypeScript recém-gerado.

1. Em `.github/copilot-instructions.md`, localize a seção intitulada **Code formatting guidance**, que deve estar por volta da linha 35.
2. Adicione o seguinte como seu último item:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

O arquivo será salvo automaticamente.

## Usar a orientação atualizada

O Copilot CLI carrega instruções do repositório quando uma conversa começa. Depois de salvar as instruções atualizadas, saia e retome a conversa de filtragem para que o Copilot comece com essa nova orientação sem perder o contexto do recurso.

1. Se a conversa de filtragem ainda estiver aberta, digite `/exit` para fechá-la. O Copilot CLI salva as conversas automaticamente.
2. Na raiz do repositório na branch `game-filters-cli`, retome a conversa salva:

   ```bash
   copilot --resume
   ```

   Se for solicitado, selecione a conversa de filtragem e confirme que a branch `game-filters-cli` está selecionada.
3. Peça ao Copilot para aplicar a orientação atualizada:

   ```plaintext
   Acabamos de atualizar nossas instruções e a orientação de código. Você pode atualizar o código que gerou para seguir essa orientação?
   ```

4. Digite `/diff` e leia os arquivos TypeScript alterados. Observe os comentários TSDoc recém-gerados e confirme que eles explicam o código com precisão.

## Resumo e próximos passos

Você explorou como o Copilot CLI coleta contexto a partir de arquivos de instrução e aplicou um novo padrão ao seu recurso. Especificamente, você:

- explorou como instruções do repositório e arquivos de instrução com escopo por caminho chegam ao agente.
- atualizou o arquivo de instruções para garantir que padrões de codificação sejam seguidos.
- viu o impacto dos arquivos de instrução no código.

Em seguida, você [personalizará e executará a skill reutilizável `quality-checks`][next-lesson] para garantir que lint e testes sejam executados de forma consistente.

## Recursos

- [Adicionar instruções personalizadas para o Copilot CLI][instruction-files]
- [Suporte a instruções personalizadas][custom-instructions-support]
- [Melhores práticas para criar instruções personalizadas][instructions-best-practices]
- [Awesome Copilot — uma coleção de arquivos de instrução e outros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
