---
title: Criar experiências incorporadas de assinatura eletrônica e documento
description: Saiba como usar as APIs da Adobe Sign para incorporar experiências de assinatura eletrônica e documentos em suas plataformas da Web e sistemas de gerenciamento de conteúdo e documentos
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7489.jpg
kt: 7489
exl-id: db300cb9-6513-4a64-af60-eadedcd4858e
source-git-commit: f015bd7ea1a25772a12cd0852d452d120f205a5c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Criar experiências incorporadas de assinatura eletrônica e documento

Saiba como usar as APIs da Adobe Sign para incorporar experiências de assinatura eletrônica e documentos em suas plataformas da Web e sistemas de gerenciamento de conteúdo e documentos. Há quatro partes neste tutorial prático descrito nos links abaixo:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="embeddedesignature.md#part1">
        <img alt="Do que você vai precisar" src="assets/embeddedesignature/EmbedPart1_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part1"><strong>Parte 1: Do que você vai precisar</strong></a>
    </div>
  </td>
  <td>
    <a href="embeddedesignature.md#part2">
        <img alt="Parte 2: Baixa/Sem código — o poder dos formulários da Web" src="assets/embeddedesignature/EmbedPart2_thumb.png" />
    </a>
    <div>
    <a href="embeddedesignature.md#part2"><strong>Parte 2: Baixa/Sem código — o poder dos formulários da Web</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part3">
      <img alt="Parte 3: Enviar contrato com um formulário, mesclar dados" src="assets/embeddedesignature/EmbedPart3_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part3"><strong>Parte 3: Enviar contrato com um formulário e mesclar dados</strong></a>
    </div>
  </td>
  <td>
   <a href="embeddedesignature.md#part4">
      <img alt="Parte 4: Incorporar experiência de assinatura, redirecionamentos e muito mais" src="assets/embeddedesignature/EmbedPart4_thumb.png" />
   </a>
    <div>
    <a href="embeddedesignature.md#part4"><strong>Parte 4: Incorporar experiência de assinatura, redirecionamentos e muito mais</strong></a>
    </div>
  </td>
</tr>
</table>

## Parte 1: Do que você vai precisar {#part1}

Na parte 1, você aprenderá como começar com tudo o que precisa para as partes 2 a 4. Vamos começar com a obtenção de credenciais de API.

* [Conta de desenvolvedor do Adobe Sign](https://acrobat.adobe.com/br/pt/sign/developer-form.html)
* [Código inicial](https://github.com/benvanderberg/adobe-sign-api-tutorial)
* [Código VS (ou editor de sua escolha)](https://code.visualstudio.com)
* Python 3.x
   * Mac — Homebreu
   * Linux — Instalador integrado
   * Janelas — Chocolatey
   * Todos — https://www.python.org/downloads/

## Parte 2: Baixa/Sem código — o poder dos formulários da Web {#part2}

Na parte 2, você explorará a opção de baixo/sem código ao usar formulários da Web. É sempre uma boa ideia ver se você pode evitar escrever código no início.

1. Acesse o Adobe Sign com sua conta de desenvolvedor.
1. Clique em **Publicar um formulário da Web** na página inicial.

   ![Captura de tela da página inicial do Adobe Sign](assets/embeddedesignature/embed_1.png)

1. Crie seu contrato.

   ![Captura de tela de como criar um formulário da Web](assets/embeddedesignature/embed_2.png)

1. Incorpore seu contrato em uma página HTML simples.
1. Experimente adicionar parâmetros de consulta dinamicamente.

   ![Captura de tela da adição de parâmetros de consulta](assets/embeddedesignature/embed_3.png)

## Parte 3: Enviar contrato com um formulário e mesclar dados {#part3}

Na parte 3, você criará contratos dinamicamente.

Primeiro, você precisará estabelecer acesso. Com o Adobe Sign, há duas maneiras de se conectar via API. Tokens OAuth &amp; Chaves de integração. A menos que você tenha um motivo muito específico para usar o OAuth com seu aplicativo, você deverá explorar as Chaves de integração primeiro.

1. Selecione **Chave de integração** no menu **Informações da API** na guia **Conta** no Adobe Sign.

   ![Captura de tela de onde encontrar a chave de integração](assets/embeddedesignature/embed_4.png)

Agora que você tem acesso e pode interagir com a API, veja o que você pode fazer com a API.

1. Navegue até [Métodos da API REST da Adobe Sign Versão 6](http://adobesign.com/public/docs/restapi/v6).

   ![Captura de tela de navegação pelos Métodos da API REST da Adobe Sign versão 6](assets/embeddedesignature/embed_5.png)

1. Use o token como um valor &quot;portador&quot;.

   ![Captura de tela do valor do portador](assets/embeddedesignature/embed_6.png)

Para enviar seu primeiro contrato, é melhor entender como usar a API.

1. Crie um documento transitório e envie-o.

>[!NOTE]
>
>As chamadas de solicitação baseadas em JSON têm as opções &quot;Modelo&quot; e &quot;Esquema de modelo mínimo&quot;. Isso oferece especificações e um conjunto de carga mínima.

![Captura de tela da criação de um documento transitório](assets/embeddedesignature/embed_7.png)

Depois de enviar um contrato pela primeira vez, você estará pronto para adicionar a lógica. É sempre uma boa ideia estabelecer alguns auxiliares para minimizar a repetição. Estes são alguns exemplos:

**Validação**

![Captura de tela da lógica de validação](assets/embeddedesignature/embed_8.png)

**Cabeçalhos/Autenticação**

![Captura de tela de cabeçalhos/lógica de autenticação](assets/embeddedesignature/embed_9.png)

**URI base**

![Captura de tela da lógica do URI base](assets/embeddedesignature/embed_10.png)

Esteja ciente de onde os documentos do Transient caem no grande esquema do ecossistema do Sign.
Transitório -> Contrato
Transitório -> Modelo -> Contrato
Transitório -> Widget -> Contrato

Este exemplo usa um modelo como a origem do documento. Essa é geralmente a melhor rota, a menos que você tenha um motivo sólido para gerar documentos para assinatura dinamicamente (por exemplo, código herdado ou geração de documento).

O código é bastante simples; ele usa um documento da biblioteca (modelo) para a origem do documento. O primeiro e o segundo signatários são atribuídos dinamicamente. O estado `IN_PROCESS` significa que o documento está sendo enviado imediatamente. Além disso, `mergeFieldInfo` é aproveitado para preencher campos dinamicamente.

![Captura de tela do código para adicionar assinaturas dinamicamente](assets/embeddedesignature/embed_11.png)

## Parte 4: Incorporar experiência de assinatura, redirecionamentos e muito mais {#part4}

Em muitos casos, você pode permitir que o participante acionador assine imediatamente um contrato. Isso é útil para aplicativos e quiosques voltados para o cliente.

Se você não deseja que o primeiro email de envio seja acionado, uma maneira fácil é gerenciar o comportamento é com uma modificação na chamada da API.

![Captura de tela do código para não acionar o envio de email](assets/embeddedesignature/embed_12.png)

Veja como controlar o redirecionamento pós-assinatura:

![Captura de tela do código para controlar o redirecionamento pós-assinatura](assets/embeddedesignature/embed_13.png)

Após atualizar o processo de criação do contrato, a etapa final está gerando o URL de assinatura. Essa chamada também é bastante direta e gera um URL que um signatário pode usar para acessar sua parte do processo de assinatura.

![Captura de tela do código para gerar um URL do signatário](assets/embeddedesignature/embed_14.png)

>[!NOTE]
>
>Observe que a chamada de criação do contrato é tecnicamente assíncrona. Isso significa que uma chamada de contrato &#39;POST&#39; pode ser feita, mas o contrato ainda não está pronto. A melhor prática é estabelecer um ciclo de repetição. Use uma nova tentativa ou seja qual for a melhor prática para o seu ambiente.

![Captura de tela dizendo que é a melhor prática estabelecer um loop de repetição](assets/embeddedesignature/embed_15.png)

Quando tudo é reunido, a solução é bastante simples. Você está fazendo um contrato e gerando um URL de assinatura para o signatário clicar e começar o ritual de assinatura.

### Tópicos adicionais

* [Eventos JS](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/events.md)
* Eventos do Webhook
   * [API REST](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/webhooks/createWebhook)
   * [Webhooks no Adobe Sign v6](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/webhooks.md)
* [Reativar e-mails de solicitação (com eventos)](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/updateAgreement)
* [Substituir tempo limite por uma nova tentativa](https://stackoverflow.com/questions/23267409/how-to-implement-retry-mechanism-into-python-requests-library)

   <br> 
* Lembretes personalizados
   * Com a criação inicial

      ![Captura de tela da navegação para o Power Automate](assets/embeddedesignature/embed_16.png)

   * Ou adicione um [em andamento](https://sign-acs.na1.echosign.com/public/docs/restapi/v6#!/agreements/createReminderOnParticipant)

## Recursos adicionais

http://bit.ly/Summit21-T126

Inclui:
* Conta de desenvolvedor do Adobe Sign
* Documentos de API da Adobe Sign
* Código de exemplo
* Código do Visual Studio
* Python
