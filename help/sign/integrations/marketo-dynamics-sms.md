---
title: Enviar notificações usando o Adobe Sign para Microsoft Dynamics 365 e Marketo
description: Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para que o signatário saiba que um contrato está a caminho
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: bcddb0ee106239f2786debaed908b2a2ec5ce792
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Enviar notificações usando o Adobe Sign para Microsoft Dynamics 365 e Marketo

Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para que o signatário saiba que um contrato está a caminho usando o Adobe Sign, o Adobe Sign para Microsoft Dynamic, o Marketo e o Marketo Microsoft Dynamics Sync. Para enviar notificações da Marketo, compre ou configure um recurso de gerenciamento de SMS da Marketo. Esta apresentação usa [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas outras soluções de SMS da Marketo estão disponíveis.

## Pré-requisitos

1. Instale o Marketo Microsoft Dynamics Sync.

   Informações e o plug-in mais recente para o Microsoft Dynamics Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instale o Adobe Sign para Microsoft Dynamics.

   Informações sobre este plug-in estão disponíveis [aqui.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Microsoft Dynamics Sync e do Adobe Sign for Dynamics estiverem concluídas, duas novas opções serão exibidas no Marketo Admin Terminal.

![Admin.](assets/adminTerminal.png)

* Clique em **[!UICONTROL Sincronização de Entidades do Dynamics]**.

   A sincronização deve ser desativada antes de sincronizar entidades personalizadas. Clique em **[!UICONTROL Sincronizar esquema]** se esta for a primeira vez. Caso contrário, clique em **[!UICONTROL Atualizar Esquema]**.

   ![Atualizar](assets/refreshSchema.png)

## Sincronizar o objeto personalizado

1. No lado direito, localize os objetos personalizados [!UICONTROL Lead], [!UICONTROL Contact] e [!UICONTROL Account].

   * **[!UICONTROL Ative]** Sincronizar para os objetos em Lead se quiser acionar quando um Lead for adicionado a um contrato no Dynamics.

   * **[!UICONTROL Ative]** Sincronizar para os objetos em Contato se quiser acionar quando um Contato for adicionado a um contrato no Dynamics.

   * **[!UICONTROL Ative]** Syncfor the objects em Account (Conta) se quiser acionar quando uma Conta for adicionada a um contrato no Dynamics.

   * **Ative** Syncfor the Agreement object (Sincronizar) no item Parent (Lead, Contact ou Account) desejado.

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. Na nova janela, selecione as propriedades desejadas em Contrato.

   Ative as caixas em **[!UICONTROL Restrição]** e **[!UICONTROL Acionador]** para expô-las às suas Atividades de marketing.

   ![Sincronização personalizada 1](assets/entitySync1.png)

   ![Sincronização personalizada 2](assets/entitySync2.png)

1. Reative a sincronização após ativar a sincronização nos objetos personalizados.

   Volte para o [!UICONTROL Admin Terminal], clique em **[!UICONTROL Microsoft Dynamics]** e, em seguida, clique em **[!UICONTROL Ativar Sincronização]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Ativar global](assets/enableGlobalDynamics.png)

## Criar o programa

1. Em [!UICONTROL Atividades de marketing], clique com o botão direito do mouse em **[!UICONTROL Atividades de marketing]** na barra esquerda, selecione **[!UICONTROL Nova pasta da campanha]** e nomeie-a.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito do mouse na pasta criada, selecione **[!UICONTROL Novo programa]** e dê um nome a ela.

   Deixe tudo o resto como padrão e clique em **[!UICONTROL Criar]**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo Programa 2](assets/newProgram2.png)

## Configurar [!DNL Twilio] SMS

Primeiro, verifique se você tem uma conta [!DNL Twilio] ativa e adquiriu os recursos de SMS necessários.

Configurar o Marketo - [!DNL Twilio] SMS webhook requer três [!DNL Twilio] parâmetros da sua conta.

* SID da conta
* Token da conta
* Número de telefone Twilio

Recupere esses parâmetros da sua conta, agora abra a instância do Marketo.

1. Clique em **[!UICONTROL Admin]** no canto superior direito.

   ![Admin.](assets/adminTab.png)

1. Clique em **[!UICONTROL Webhooks]** e, em seguida, clique em **[!UICONTROL Novo Webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **[!UICONTROL Nome do Webhook]** e **[!UICONTROL Descrição]**.

1. Insira o seguinte URL e certifique-se de substituir as `ACCOUNT_SID` e `AUTH_TOKEN` pelas credenciais [!DNL Twilio].

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecione **[!UICONTROL POST]** como o tipo de Solicitação.

1. Insira o seguinte **Modelo** e substitua `MY_TWILIO_NUMBER` pelo número de telefone [!DNL Twilio] e `YOUR_MESSAGE` por uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina **[!UICONTROL Codificação do token de solicitação]** como *Formulário/URL*.

1. Defina o Tipo de resposta como *JSON* e clique em **[!UICONTROL Salvar]**.

## Configurar o Acionador da Campanha Inteligente

1. Na seção Atividades de marketing, clique com o botão direito do mouse no programa que você criou e selecione **[!UICONTROL Nova Campanha Inteligente]**.

   ![Campanha inteligente 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **[!UICONTROL Criar]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Você deve ver vários acionadores disponíveis para uso na pasta Microsoft.

1. Clique e arraste **[!UICONTROL Adicionado ao contrato]** para a **[!UICONTROL Lista inteligente]** e, em seguida, adicione as restrições que deseja ter no acionador.

   ![Adicionado ao contrato](assets/addedToAgreementDynamics.png)

## Configurar o Fluxo de Campanha Inteligente

1. Clique na guia **[!UICONTROL Fluxo]** na [!UICONTROL Campanha inteligente].

   Procure e arraste o fluxo **Chamar webhook** para a tela e selecione o webhook criado na seção anterior.

   ![Ligar para o Webhook](assets/callWebhook.png)

1. Sua campanha de notificação por SMS para clientes potenciais adicionados a um contrato está configurada.
>[!TIP]
>
>Este tutorial é parte do curso [Acelere os ciclos de vendas com o Adobe Sign for Microsoft Dynamics e o Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!