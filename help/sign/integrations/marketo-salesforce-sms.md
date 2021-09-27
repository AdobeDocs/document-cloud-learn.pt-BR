---
title: Enviar notificações usando o Adobe Sign para Salesforce e Marketo
description: Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para que o signatário saiba que um contrato está a caminho
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Enviar notificações usando o Adobe Sign para Salesforce e Marketo

Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para que o signatário saiba que um contrato está em andamento usando o Adobe Sign, o Adobe Sign para Salesforce, o Marketo e o Marketo Salesforce Sync. Para enviar notificações da Marketo, compre ou configure um recurso de gerenciamento de SMS da Marketo. Esta apresentação usa [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas outras soluções de SMS da Marketo estão disponíveis.

## Pré-requisitos

1. Instale o Marketo Salesforce Sync.

   Informações e o plug-in mais recente para Sincronização do Salesforce estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instalar o Adobe Sign para Salesforce.

   Informações sobre este plug-in estão disponíveis [aqui.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações Marketo Salesforce Sync e Adobe Sign for Salesforce estiverem concluídas, várias novas opções serão exibidas no Marketo Admin Terminal.

![Admin.](assets/adminTab.png)

![Sincronização de objeto](assets/salesforceAdmin.png)

1. Clique em **Sincronizar esquema** se esta for a primeira vez. Caso contrário, clique em **Atualizar Esquema**.

   ![Atualizar](assets/refreshSchema1.png)

1. Se a sincronização global estiver em execução, desative clicando em **Desativar sincronização global**.

   ![Desabilitar](assets/disableGlobal.png)

1. Clique em **Atualizar Esquema**.

   ![Atualizar 2](assets/refreshSchema2.png)

## Sincronizar os objetos personalizados

No lado direito, consulte Objetos personalizados baseados em Lead, Contato e Conta.

**Ative** Sincronizar para os objetos em Lead se quiser acionar quando um Lead for adicionado a um contrato no Salesforce.

**Ative** Sincronizar para os objetos em Contato se quiser acionar quando um Contato for adicionado a um contrato no Salesforce.

**Ative** Syncfor the objects em Account (Conta) se quiser acionar quando uma Conta for adicionada a um contrato no Salesforce.

1. **Ative o** Syncfor the custom objects mostrados sob o Principal desejado (Lead, Contato ou Conta).

   ![Objetos personalizados](assets/customObjects.png)

1. Os seguintes ativos mostram como **Ativar sincronização**.

   ![Sincronização personalizada 1](assets/customObjectSync1.png)

   ![Sincronização personalizada 2](assets/customObjectSync2.png)

1. Quando terminar de ativar a sincronização em Objetos personalizados, reative a sincronização.

   ![Ativar global](assets/enableGlobal.png)

## Criar o programa

1. Na seção Atividades de marketing da Marketo, clique com o botão direito do mouse em **Atividades de marketing** na barra esquerda, selecione **Nova pasta da campanha** e dê um nome a ela.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito do mouse na pasta criada, selecione **Novo programa** e dê um nome a ela. Deixe tudo o resto como padrão e clique em **Criar**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo Programa 2](assets/newProgram2.png)

## Configurar Twilio SMS

Primeiro, verifique se você tem uma conta ativa do Twilio e adquiriu os recursos de SMS necessários.

Configurar o webhook Marketo - Twilio SMS requer três parâmetros Twilio da sua conta.

- SID da conta
- Token da conta
- Número de telefone Twilio

Recupere esses parâmetros da sua conta, agora abra a instância do Marketo.

1. Clique em **Admin** no canto superior direito.

   ![Admin.](assets/adminTab.png)

1. Clique em **Webhooks** e, em seguida, em **Novo Webhook**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **Nome do Webhook** e **Descrição**.

1. Insira o seguinte URL e certifique-se de substituir **[ACCOUNT_SID]** e **[AUTH_TOKEN]** pelas suas credenciais do Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecione **POST** como o tipo de Solicitação.

1. Insira o seguinte **Modelo** e certifique-se de substituir **[MY_TWILIO_NUMBER]** pelo número de telefone Twilio e **[YOUR_MESSAGE]** por uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina a Codificação do token de solicitação como Form/URL.

1. Defina o Tipo de resposta como JSON e clique em **Salvar**.

## Configurar o Acionador da Campanha Inteligente

1. Na seção Atividades de marketing, clique com o botão direito do mouse no programa que você criou e selecione **Nova Campanha Inteligente**.

   ![Campanha inteligente 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **Criar**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Se a configuração da Sincronização de objeto personalizada foi feita corretamente, você deverá ver os seguintes acionadores disponíveis para uso na pasta do Salesforce.

1. Clique em e arraste Adicionado ao contrato para a lista inteligente. Adicione todas as restrições que deseja ter no acionador.

   ![Adicionado ao contrato 2](assets/addedToAgreement2.png)

## Configurar o Fluxo de Campanha Inteligente

1. Clique na guia **Fluxo** na Campanha inteligente. Procure e arraste o fluxo **Chamar webhook** para a tela e selecione o webhook criado na seção anterior.

   ![Ligar para o Webhook](assets/callWebhook.png)

1. Sua campanha de notificação por SMS para clientes potenciais adicionados a um contrato está configurada.

>[!TIP]
>
>Este tutorial é parte do curso [Acelere os ciclos de vendas com o Adobe Sign para Salesforce e o Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!