---
title: Enviar notificações usando o Acrobat Sign para Salesforce e Marketo
description: Saiba como enviar uma mensagem de texto, email ou notificação por push para permitir que o signatário saiba que um contrato está a caminho
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Enviar notificações usando o Acrobat Sign para Salesforce e Marketo

Saiba como enviar uma mensagem de texto, email ou notificação por push para permitir que o signatário saiba que um contrato está a caminho usando o Acrobat Sign, o Acrobat Sign para Salesforce, o Marketo e o Marketo Salesforce Sync. Para enviar notificações do Marketo, primeiro você precisa comprar ou configurar um recurso de gerenciamento de SMS do Marketo. Este passo a passo usa [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas outras soluções de SMS da Marketo estão disponíveis.

## Pré-requisitos

1. Instale o Marketo Salesforce Sync.

   Informações e o plug-in mais recente para o Salesforce Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instale o Acrobat Sign para Salesforce.

   Informações sobre este plug-in estão disponíveis [aqui.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Salesforce Sync e do Acrobat Sign para Salesforce forem concluídas, várias novas opções serão exibidas no Marketo Admin Terminal.

![Admin.](assets/adminTab.png)

![Sincronização de Objetos](assets/salesforceAdmin.png)

1. Clique em **Esquema de sincronização** se esta é a sua primeira vez. Caso contrário, clique em **Atualizar Esquema**.

   ![Atualizar](assets/refreshSchema1.png)

1. Se a sincronização global estiver em execução, desative clicando em **Desabilitar Sincronização Global**.

   ![Desabilitar](assets/disableGlobal.png)

1. Clique em **Atualizar Esquema**.

   ![Atualização 2](assets/refreshSchema2.png)

## Sincronizar os objetos personalizados

No lado direito, consulte objetos personalizados baseados em lead, contato e conta.

**Ativar sincronização** para os objetos em Lead, se desejar acionar quando um Lead for adicionado a um contrato no Salesforce.

**Ativar sincronização** para os objetos em Contato, se você deseja acionar quando um Contato é adicionado a um contrato no Salesforce.

**Ativar sincronização** para os objetos em Conta, se você deseja acionar quando uma Conta é adicionada a um contrato no Salesforce.

1. **Ativar sincronização** para os objetos personalizados exibidos sob o Pai desejado (Lead, Contato ou Conta).

   ![Objetos personalizados](assets/customObjects.png)

1. Os seguintes ativos mostram como **Ativar sincronização**.

   ![Sincronização personalizada 1](assets/customObjectSync1.png)

   ![Sincronização personalizada 2](assets/customObjectSync2.png)

1. Quando terminar de ativar a sincronização em Objetos personalizados, reative a sincronização.

   ![Ativar Global](assets/enableGlobal.png)

## Criar o programa

1. Na seção Atividades de marketing do Marketo, clique com o botão direito do mouse em **Atividades de marketing** na barra esquerda, selecione **Nova Pasta de Campanha** e dê um nome.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito do mouse na pasta criada e selecione **Novo programa** e dê um nome. Deixe todo o resto como padrão e clique em **Criar**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo programa 2](assets/newProgram2.png)

## Configurar o Twilio SMS

Primeiro, certifique-se de ter uma conta ativa do Twilio e comprou os recursos de SMS que você precisa.

Configurar o webhook Marketo - Twilio SMS requer três parâmetros Twilio de sua conta.

- SID da conta
- Token da conta
- Número de telefone do Twilio

Recupere esses parâmetros da sua conta, agora abra sua instância do Marketo.

1. Clique em **Admin** no canto superior direito.

   ![Admin.](assets/adminTab.png)

1. Clique em **Webhooks**, depois **Novo webhook**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **Nome do webhook** e **Descrição**.

1. Insira o seguinte URL e substitua o **[ACCOUNT_SID]** e **[AUTH_TOKEN]** com suas credenciais do Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecionar **POST** como seu tipo de Solicitação.

1. Insira o seguinte **Modelo** e certifique-se de substituir **[MY_TWILIO_NUMBER]** com seu número de telefone do Twilio e **[SUA_MENSAGEM]** com uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina a Codificação do token de solicitação como Formulário/URL.

1. Defina o Tipo de resposta como JSON e clique em **Salvar**.

## Configurar o Gatilho da Campanha Inteligente

1. Na seção Atividades de marketing, clique com o botão direito do mouse no programa que você criou e selecione **Nova Campanha Inteligente**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **Criar**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Se a configuração para Sincronização de objeto personalizado foi feita corretamente, você deve ver os seguintes acionadores disponíveis para uso na pasta do Salesforce.

1. Clique e arraste Adicionado ao contrato para a Smart List. Adicione as restrições que deseja ter no acionador.

   ![Adicionado ao contrato 2](assets/addedToAgreement2.png)

## Configurar o fluxo de campanha inteligente

1. Clique no botão **Fluxo** no Smart Campaign. Pesquise e arraste o **Chamar Webhook** vá para a tela e selecione o webhook criado na seção anterior.

   ![Chamar Webhook](assets/callWebhook.png)

1. Sua campanha de aviso por SMS para clientes potenciais adicionados a um contrato já foi configurada.

>[!TIP]
>
>Este tutorial faz parte do curso [Agilizar os ciclos de vendas com o Acrobat Sign para Salesforce e Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!