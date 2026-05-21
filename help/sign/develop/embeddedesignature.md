---
title: Criar experiências incorporadas de assinatura eletrônica e documento
description: Saiba como usar as APIs do Acrobat Sign para incorporar experiências de assinatura eletrônica e de documento em suas plataformas Web e sistemas de gerenciamento de conteúdo e documentos
feature: Integrations, Workflow
role: Developer
level: Intermediate
topic: Integrations
jira: KT-7489
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
TQID: https://experienceleague.adobe.com/hpoT07uqXklt0yT3-oD6AW8mWcbGxqalTao-5lc6BCc
product_v2: id: b12c730b-5ddb-4a2d-ba42-da774988b909id: c1c5fb98-9105-44ed-9df1-9e04d062a784id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
feature_v2: id: a1028f9a-6dbc-4a4f-adf5-eb9f85a408a6
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: d92345097c162b68b9d8405122534371c87c5f1a
workflow-type: tm+mt
source-wordcount: 917
ht-degree: 1%

---

# Criar assinatura eletrônica incorporada e experiências de documento

Saiba como usar as APIs do Acrobat Sign para incorporar experiências de assinatura eletrônica e de documento em plataformas Web e sistemas de gerenciamento de conteúdo e documentos. Há quatro partes neste tutorial prático.

## Parte 1: Do que você precisa

Na parte 1, saiba como começar a usar tudo o que você precisa para as partes 2 a 4. Vamos começar obtendo credenciais de API.

+++Exibir detalhes sobre como obter credenciais de API

* [Conta de desenvolvedor do Acrobat Sign](https://www.adobe.com/acrobat/business/developer-form.html)
* [Código Inicial](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [Código VS (ou editor de sua escolha)](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebrew
   * Linux — Instalador integrado
   * Windows — Chocolatey
   * All — https://www.python.org/downloads/

+++

## Parte 2: Código baixo/nulo — o poder dos formulários web

Na parte 2, explore a opção de baixo valor/sem código do uso de formulários web. É sempre uma boa ideia ver se você pode evitar escrever código no início.

+++Exibir detalhes sobre como criar um formulário da Web

1. Acesse o Acrobat Sign com sua conta de desenvolvedor.

1. Selecione **Publish um formulário web** na página inicial.

   ![Captura de tela da página inicial do Acrobat Sign](assets/embeddedesignature/embed_1.png)

1. Crie seu contrato.

   ![Captura de tela de como criar um formulário da Web](assets/embeddedesignature/embed_2.png)

1. Insira seu contrato em uma página de HTML simples.

1. Experimente adicionar parâmetros de consulta dinamicamente.

   ![Captura de tela da adição de parâmetros de consulta](assets/embeddedesignature/embed_3.png)

+++

## Parte 3: Enviar contrato com um formulário e mesclar dados

Na parte 3, crie contratos dinamicamente.

+++Exibir detalhes sobre como criar contratos dinamicamente

Primeiro, você precisa estabelecer o acesso. Com o Acrobat Sign, há duas maneiras de se conectar por meio da API. Tokens OAuth e Chaves de Integração. A menos que você tenha um motivo muito específico para usar o OAuth com o aplicativo, você deve explorar as Chaves de integração primeiro.

1. Selecione **Chave de integração** no menu **Informações de API** na guia **Conta** do Acrobat Sign.

   ![Captura de tela de onde encontrar a chave de integração](assets/embeddedesignature/embed_4.png)

Agora que você tem acesso e pode interagir com a API, veja o que você pode fazer com a API.

1. Navegue até os [Métodos da ](http://adobesign.com/public/docs/restapi/v6) da API REST Versão 6.

   ![Captura de tela de navegação dos Métodos da Acrobat Sign REST API Versão 6](assets/embeddedesignature/embed_5.png)

1. Use o token como um valor de “portador”.

   ![Captura de tela do valor do portador](assets/embeddedesignature/embed_6.png)

Para enviar seu primeiro contrato, é melhor entender como usar a API.

1. Crie um Documento temporário e envie-o.

>[!NOTE]
>
>As chamadas de solicitação baseadas em JSON têm uma opção “Modelo” e “Esquema de modelo mínimo”. Isso fornece especificações e um conjunto mínimo de carga útil.

![Captura de tela da criação de um Documento Temporário](assets/embeddedesignature/embed_7.png)

Depois de enviar um contrato pela primeira vez, você estará pronto para adicionar a lógica. É sempre uma boa ideia estabelecer alguns auxiliares para minimizar a repetição. Veja alguns exemplos:

**Validação**

![Captura de tela da lógica de validação](assets/embeddedesignature/embed_8.png)

**Cabeçalhos/Autenticação**

![Captura de tela de cabeçalhos/lógica de autenticação](assets/embeddedesignature/embed_9.png)

**URI Base**

![Captura de tela da lógica do URI base](assets/embeddedesignature/embed_10.png)

Lembre-se de onde os Documentos transitórios pousam no esquema geral do ecossistema do Sign.
Temporário -> Contrato
Temporário -> Modelo -> Contrato
Temporário -> Widget -> Contrato

Este exemplo usa um modelo como nossa origem de documento. Geralmente, esse é o melhor caminho, a menos que você tenha um motivo sólido para gerar dinamicamente documentos para assinatura (por exemplo, código legado ou geração de documento).

O código é bastante simples; ele usa um documento da biblioteca (modelo) para a origem do documento. O primeiro e o segundo signatários são atribuídos dinamicamente. O estado `IN_PROCESS` significa que o documento está sendo enviado imediatamente. Além disso, o `mergeFieldInfo` é aproveitado para preencher campos dinamicamente.

![Captura de tela de código para adicionar assinaturas dinamicamente](assets/embeddedesignature/embed_11.png)

+++

## Parte 4: incorpore experiência de assinatura, redirecionamentos e muito mais

Em muitas situações, você pode permitir que o participante de acionamento assine imediatamente um contrato. Isso é útil para aplicativos e quiosques voltados para o cliente.

+++Exibir detalhes sobre como incorporar a experiência de assinatura

Se você não quiser que o primeiro email de envio seja acionado, uma maneira fácil é gerenciar o comportamento é com uma modificação na chamada de API.

![Captura de tela de código para não disparar o envio de email](assets/embeddedesignature/embed_12.png)

Veja como controlar o redirecionamento pós-assinatura:

![Captura de tela do código para controlar o redirecionamento pós-assinatura](assets/embeddedesignature/embed_13.png)

Depois de atualizar o processo de criação do contrato, a etapa final é gerar o URL de assinatura. Essa chamada também é bastante direta e gera um URL que um signatário pode usar para acessar sua parte do processo de assinatura.

![Captura de tela de código para gerar uma URL de signatário](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Observe que a chamada de criação do contrato é tecnicamente assíncrona. Isso significa que uma chamada de contrato &#39;POST&#39; pode ser feita, mas o contrato ainda não está pronto. A prática recomendada é estabelecer um loop de repetição. Use uma nova tentativa ou qualquer outra prática recomendada para seu ambiente.

![Captura de tela dizendo que é uma prática recomendada estabelecer um loop de repetição](assets/embeddedesignature/embed_15.png)

Quando tudo está pronto, a solução é bastante simples. Você está criando um contrato e gerando um URL de assinatura para que o signatário clique e comece o ritual de assinatura.

+++

## Tópicos adicionais

* [JS Events](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Eventos do Webhook
   * [API REST](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks no Acrobat Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Reativar e-mails de solicitação (com eventos)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Substituir o tempo limite por uma nova tentativa](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)
* Lembretes personalizados
   * Com a criação inicial

     ![Captura de tela de navegação para o Power Automate](assets/embeddedesignature/embed_16.png)

   * Ou adicione um [em andamento](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)
