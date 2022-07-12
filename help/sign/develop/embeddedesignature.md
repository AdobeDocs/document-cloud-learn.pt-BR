---
title: Crie assinaturas eletrônicas incorporadas e experiências em documentos
description: Saiba como usar APIs do Acrobat Sign para incorporar assinaturas eletrônicas e experiências de documentos às suas plataformas da Web e sistemas de gerenciamento de documentos e conteúdo
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: f68fc211dc315a7d7ef508787c80fbe9882fcdc3
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Crie assinaturas eletrônicas incorporadas e experiências em documentos

Saiba como usar APIs do Acrobat Sign para incorporar assinaturas eletrônicas e experiências de documentos às suas plataformas da Web e sistemas de gerenciamento de documentos e conteúdo. Há quatro partes neste tutorial prático.

## Parte 1: O que você precisa

Na parte 1, saiba como começar com tudo o que você precisa para as partes 2 a 4. Vamos começar obtendo credenciais de API.

+++Exibir detalhes sobre como obter credenciais de API

* [Conta de desenvolvedor do Acrobat Sign](https://acrobat.adobe.com/br/pt/sign/developer-form.html)
* [Código Inicial](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [Código VS (ou editor de sua escolha)](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebrew
   * Linux — Instalador integrado
   * Windows — Chocolatey
   * Todos — https://www.python.org/downloads/

+++

## Parte 2: Baixo/sem código — o poder dos formulários web

Na parte 2, explore a opção de baixo/sem código do uso de formulários web. É sempre uma boa ideia ver se você pode evitar escrever código no início.

+++Exibir detalhes sobre como criar um formulário da Web

1. Acesse o Acrobat Sign com sua conta de desenvolvedor.

1. Selecionar **Publicar um formulário da Web** na página inicial.

   ![Captura de tela da página inicial do Acrobat Sign](assets/embeddedesignature/embed_1.png)

1. Crie seu contrato.

   ![Captura de tela de como criar um formulário da Web](assets/embeddedesignature/embed_2.png)

1. Incorpore seu contrato em uma página HTML simples.

1. Experimente adicionar parâmetros de consulta dinamicamente.

   ![Captura de tela da adição de parâmetros de consulta](assets/embeddedesignature/embed_3.png)

+++

## Parte 3: Enviar contrato com um formulário e mesclar dados

Na parte 3, crie contratos de maneira dinâmica.

+++Exibir detalhes sobre como criar contratos dinamicamente

Primeiro, você precisa estabelecer o acesso. Com o Acrobat Sign, há duas maneiras de se conectar por meio da API. Tokens OAuth e chaves de integração. A menos que você tenha um motivo muito específico para usar o OAuth com seu aplicativo, você deve explorar as Chaves de integração primeiro.

1. Selecionar **Chave de integração** no **Informações da API** menu abaixo do **Conta** no Acrobat Sign.

   ![Captura de tela de onde encontrar a chave de integração](assets/embeddedesignature/embed_4.png)

Agora que você tem acesso e pode interagir com a API, veja o que pode fazer com a API.

1. Navegue até o [Métodos da Acrobat Sign REST API Versão 6](http://adobesign.com/public/docs/restapi/v6).

   ![Captura de tela dos métodos de navegação da API REST Versão 6 do Acrobat Sign](assets/embeddedesignature/embed_5.png)

1. Use o token como um valor de &quot;portador&quot;.

   ![Captura de tela do valor do portador](assets/embeddedesignature/embed_6.png)

Para enviar seu primeiro contrato, é melhor entender como usar a API.

1. Crie um Documento temporário e envie-o.

>[!NOTE]
>
>As chamadas de solicitação baseadas em JSON têm uma opção &quot;Modelo&quot; e &quot;Esquema de modelo mínimo&quot;. Isso fornece especificações e um conjunto de carga útil mínima.

![Captura de tela da criação de um Documento temporário](assets/embeddedesignature/embed_7.png)

Depois de enviar um contrato pela primeira vez, você estará pronto para adicionar a lógica. É sempre uma boa ideia estabelecer alguns auxiliares para minimizar a repetição. Estes são alguns exemplos:

**Validação**

![Captura de tela da lógica de validação](assets/embeddedesignature/embed_8.png)

**Cabeçalhos/Autenticação**

![Captura de tela de cabeçalhos/lógica de autenticação](assets/embeddedesignature/embed_9.png)

**URI Base**

![Captura de tela da lógica de URI base](assets/embeddedesignature/embed_10.png)

Lembre-se de onde os documentos transitórios estão no grande esquema do ecossistema do Sign.
Temporário -> Contrato transitório -> Modelo -> Contrato transitório -> Widget -> Contrato

Este exemplo usa um modelo como nossa fonte de documento. Geralmente, essa é a melhor rota, a menos que você tenha um motivo sólido para gerar dinamicamente documentos para assinatura (por exemplo, código herdado ou geração de documento).

O código é bastante simples; ele usa um documento da biblioteca (modelo) para a origem do documento. O primeiro e o segundo signatários são atribuídos dinamicamente. O `IN_PROCESS` estado significa que o documento está sendo enviado imediatamente. Além disso, `mergeFieldInfo` é aproveitado para preencher campos dinamicamente.

![Captura de tela do código para adicionar assinaturas dinamicamente](assets/embeddedesignature/embed_11.png)

+++

## Parte 4: Incorpore experiência de assinatura, redirecionamentos e muito mais

Em muitos casos, você pode permitir que o participante acionador assine imediatamente um contrato. Isso é útil para aplicativos e quiosques voltados para o cliente.

+++Veja detalhes sobre como incorporar a experiência de assinatura

Se você não deseja que o primeiro email de envio seja acionado, uma maneira fácil é gerenciar o comportamento é com uma modificação na chamada de API.

![Captura de tela do código para não acionar o envio de email](assets/embeddedesignature/embed_12.png)

Veja como controlar o redirecionamento pós-assinatura:

![Captura de tela do código para controlar o redirecionamento pós-assinatura](assets/embeddedesignature/embed_13.png)

Depois de atualizar o processo de criação do contrato, a etapa final é gerar o URL de assinatura. Essa chamada também é bastante direta e gera um URL que um signatário pode usar para acessar sua parte do processo de assinatura.

![Captura de tela do código para gerar um URL do signatário](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Observe que a chamada de criação do contrato é tecnicamente assíncrona. Isso significa que uma chamada de contrato &#39;POST&#39; pode ser feita, mas o contrato ainda não está pronto. A prática recomendada é estabelecer um loop de repetição. Use uma repetição ou qualquer outra prática recomendada para seu ambiente.

![Captura de tela dizendo que é prática recomendada estabelecer um loop de repetição](assets/embeddedesignature/embed_15.png)

Quando tudo é montado, a solução é bastante simples. Você está criando um contrato e gerando um URL de assinatura para o signatário clicar e começar o ritual de assinatura.

+++

## Tópicos adicionais

* [Eventos JS](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Eventos do Webhook
   * [API REST](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks no Acrobat Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Reativar e-mails de solicitação (com eventos)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Substituir Tempo Limite por uma Repetição](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)

   <br> 
* Lembretes personalizados
   * Com a criação inicial

      ![Captura de tela de navegação para o Power Automate](assets/embeddedesignature/embed_16.png)

   * Ou adicione um [em voo](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)
