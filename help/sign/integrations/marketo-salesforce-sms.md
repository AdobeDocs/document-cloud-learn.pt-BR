---
title: Enviar notificações usando o Acrobat Sign para Salesforce e Marketo
description: Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para permitir que o signatário saiba que um contrato está a caminho
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
jira: KT-7247
topic: Integrations
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: ac3334ec-b65f-4ce4-b323-884948f5e0a6
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Enviar notificações usando o Acrobat Sign para [!DNL Salesforce] e [!DNL Marketo]

Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para permitir que o signatário saiba que um contrato está a caminho usando o Acrobat Sign, o Acrobat Sign para Salesforce, o Marketo e a sincronização do Marketo Salesforce. Para enviar notificações do Marketo, primeiro você precisa comprar ou configurar um recurso de gerenciamento de SMS do Marketo. Esta apresentação usa [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas há outras soluções Marketo SMS disponíveis.

## Pré-requisitos

1. Instale o Marketo Salesforce Sync.

   Informações e o plug-in mais recente do Salesforce Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instale o Acrobat Sign para Salesforce.

   Informações sobre este plug-in estão disponíveisName [aqui.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Salesforce Sync e do Acrobat Sign for Salesforce estiverem concluídas, várias novas opções serão exibidas no Marketo Admin Terminal.

![Admin](assets/adminTab.png)

![Sincronização de objeto](assets/salesforceAdmin.png)

1. Clique em **Esquema de sincronização** se for sua primeira vez. Caso contrário, clique **Atualizar Esquema**.

   ![Atualizar](assets/refreshSchema1.png)

1. Se a sincronização global estiver em execução, desative clicando em **Desativar sincronização global**.

   ![Desabilitar](assets/disableGlobal.png)

1. Clique em **Atualizar Esquema**.

   ![Atualizar 2](assets/refreshSchema2.png)

## Sincronizar os objetos personalizados

No lado direito, consulte Objetos personalizados baseados em Lead, Contato e Conta.

**Ativar sincronização** para os objetos em Lead se desejar acionar quando um Lead for adicionado a um contrato no Salesforce.

**Ativar sincronização** para os objetos em Contato, se você deseja acionar quando um Contato é adicionado a um contrato no Salesforce.

**Ativar sincronização** para os objetos em Conta, se você deseja acionar quando uma Conta é adicionada a um contrato no Salesforce.

1. **Ativar sincronização** para os objetos personalizados exibidos na página principal desejada (lead, contato ou conta).

   ![Objetos personalizados](assets/customObjects.png)

1. Os seguintes ativos mostram como **Ativar sincronização**.

   ![Sincronização personalizada 1](assets/customObjectSync1.png)

   ![Sincronização personalizada 2](assets/customObjectSync2.png)

1. Quando terminar de ativar a sincronização nos Objetos personalizados, reative a sincronização.

   ![Ativar global](assets/enableGlobal.png)

## Criar o programa

1. Na seção Atividades de marketing do Marketo, clique com o botão direito do mouse em **Atividades de marketing** na barra esquerda, selecione **Nova Pasta de Campanha** e dê um nome a ele.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito na pasta criada, selecione **Novo programa** e dê um nome a ele. Deixe todo o resto como padrão e clique em **Criar**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo programa 2](assets/newProgram2.png)

## Configurar o Twilio SMS

Primeiro, certifique-se de ter uma conta ativa do Twilio e adquirir os recursos de SMS necessários.

Configurar o webhook Marketo - Twilio SMS requer três parâmetros do Twilio de sua conta.

- SID da conta
- Token da conta
- Número de telefone do Twilio

Recupere esses parâmetros de sua conta e abra uma instância do Marketo.

1. Clique em **Admin** no canto superior direito.

   ![Admin](assets/adminTab.png)

1. Clique em **Webhooks**, depois **Novo webhook**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **Nome do webhook** e **Descrição**.

1. Insira o seguinte URL e substitua o **[ACCOUNT_SID]** e **[AUTH_TOKEN]** com suas credenciais do Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecionar **POST** como seu tipo de Solicitação.

1. Insira o seguinte **Modelo** e certifique-se de substituir **[MY_TWILIO_NUMBER]** com seu número de telefone Twilio e **[SUA_MENSAGEM]** com uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina a codificação do token de solicitação como Formulário/URL.

1. Defina o Tipo de resposta como JSON e clique em **Salvar**.

## Configurar o acionador da campanha inteligente

1. Na seção Atividades de Marketing, clique com o botão direito do mouse no programa que você criou e selecione **Nova campanha inteligente**.

   ![Campanha inteligente 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **Criar**.

   ![Campanha inteligente 2](assets/smartCampaign3.png)

   Se a configuração da sincronização de objeto personalizado foi feita corretamente, você deve ver os seguintes acionadores disponíveis para uso na pasta Salesforce.

1. Clique e arraste Adicionado ao contrato para a Smart List. Adicione quaisquer restrições que você deseja ter no acionador.

   ![Adicionado ao Contrato 2](assets/addedToAgreement2.png)

## Configurar o fluxo de campanha inteligente

1. Clique no botão **Fluxo** na Campanha inteligente. Procure e arraste o **Ligar para Webhook** siga para a tela e selecione o webhook que você criou na seção anterior.

   ![Ligar para Webhook](assets/callWebhook.png)

1. Sua campanha de aviso por SMS para clientes potenciais adicionados a um contrato está configurada.

>[!TIP]
>
>Este tutorial é parte do curso [Acelere os ciclos de vendas com o Acrobat Sign para Salesforce e Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!