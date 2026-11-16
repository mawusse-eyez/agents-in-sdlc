---
title: "Lição 12 - Implantar o site com o GitHub Pages"
description: "Use o aplicativo GitHub Copilot para configurar um fluxo de trabalho do Pages, revisar a pull request e verificar o Space Quiz em produção."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Dê ao Space Quiz uma casa pública implantando-o com o GitHub Pages. O Copilot pode preparar o fluxo de trabalho e orientar a implantação, mas você continua responsável por revisar as alterações e confirmar que o site está em funcionamento.

Nesta lição, você vai:

- pedir ao Copilot para configurar uma implantação do GitHub Pages.
- revisar o fluxo de trabalho e a pull request antes de mesclar.
- acompanhar a implantação e verificar o site publicado.

## Cenário

O Space Quiz já está em um repositório do GitHub, mas as pessoas ainda precisam de uma maneira simples de experimentá-lo. Publicar o site de arquivo único com o GitHub Pages torna-o acessível por meio de uma URL pública, sem adicionar um servidor ou dependência de runtime.

## Pedir ao Copilot para preparar a implantação

> [!WARNING]
> Criar uma pull request pode confirmar e enviar código. Revise as configurações de aprovação e o repositório de destino antes de enviar este prompt. Com **Approve all**, não espere uma confirmação separada.

Na sessão do aplicativo Copilot para `space-quiz`, envie este prompt:

```plaintext
Prepare uma implantação do GitHub Pages para este repositório. Crie um fluxo de trabalho do GitHub Actions que compile o site, se necessário, e implante-o no GitHub Pages depois que as alterações chegarem ao branch padrão. Adicione um README descrevendo o aplicativo e como executá-lo localmente, se ainda não existir. Crie uma pull request com essas alterações e informe o link e quaisquer configurações ou permissões necessárias do Pages. Não mescle, não habilite mesclagem automática, não altere as configurações do Pages nem implante. Pare e aguarde minha revisão.
```

## Revisar o fluxo de trabalho e a pull request

1. Confirme que o README foi adicionado somente se o repositório ainda não tiver um.
2. Revise as alterações da pull request, incluindo as etapas de build e implantação do fluxo de trabalho, gatilhos e permissões.
3. Confirme que o fluxo de trabalho implanta a partir do branch padrão, e não a partir de uma pull request não mesclada.
4. Solicite correções e revise o diff atualizado. Aguarde que os checks da pull request sejam aprovados antes de autorizar a fusão.

## Autorizar a mesclagem e a implantação

> [!WARNING]
> O prompt a seguir autoriza o agente a mesclar a pull request revisada, alterar as configurações do Pages do repositório e publicar o site. Envie-o somente depois de concluir sua revisão e confirmar o repositório e a pull request. As configurações de aprovação podem permitir essas ações sem outra confirmação.

Substitua `<PR_NUMBER>` pelo número da pull request revisada e envie este prompt separado:

```plaintext
Eu revisei a pull request <PR_NUMBER> neste repositório e autorizo sua mesclagem e implantação. Habilite o GitHub Pages usando o GitHub Actions, mescle essa pull request somente depois que os checks obrigatórios passarem e monitore a implantação até que ela seja bem-sucedida. Informe a URL final do site em produção. Se você não tiver permissão para habilitar o Pages ou mesclar, me diga exatamente o que preciso aprovar ou fazer; não informe êxito até que o site esteja em produção.
```

![Diagrama em três etapas: uma pull request do space-quiz mesclada; uma execução bem-sucedida do GitHub Actions Deploy website com as etapas Build website, Upload artifact e Deploy to Pages; e o Space Quiz em execução em yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

## Verificar a implantação

1. Siga a execução de implantação do GitHub Actions até que ela seja bem-sucedida.
2. Abra a URL informada e confirme que o Space Quiz foi carregado.

Se o agente não conseguir habilitar o Pages ou mesclar a pull request, siga as instruções específicas que ele fornecer. Não considere a tarefa concluída até que a implantação tenha sido bem-sucedida e o site em produção carregue corretamente.

## Resumo e próximos passos

Seu Space Quiz agora está disponível como site ao vivo, e você verificou a implantação em vez de confiar apenas no relatório do agente. Continue para a [Lição 13: revisão e próximos passos][next-lesson].

[next-lesson]: ../13-review/
