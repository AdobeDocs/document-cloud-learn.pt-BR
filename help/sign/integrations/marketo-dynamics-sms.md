---
title: Enviar notificações usando o Acrobat Sign para Microsoft Dynamics 365 e Marketo
description: Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para permitir que o signatário saiba que um contrato está a caminho
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7249
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Enviar notificações usando o Acrobat Sign para Microsoft Dynamics 365 e Marketo

Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para informar ao signatário que um contrato está a caminho usando o Acrobat Sign, o Acrobat Sign para Microsoft Dynamic, o Marketo e o Marketo Microsoft Dynamics Sync. Para enviar notificações do Marketo, primeiro você precisa comprar ou configurar um recurso de gerenciamento de SMS do Marketo. Esta apresentação usa [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas há outras soluções Marketo SMS disponíveis.

## Pré-requisitos

1. Instale o Marketo Microsoft Dynamics Sync.

   Informações e o plug-in mais recente do Microsoft Dynamics Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instale o Acrobat Sign para Microsoft Dynamics.

   Informações sobre este plug-in estão disponíveisName [aqui.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Microsoft Dynamics Sync e do Acrobat Sign for Dynamics estiverem concluídas, duas novas opções serão exibidas no Admin Terminal do Marketo.

![Admin](assets/adminTerminal.png)

* Clique em **[!UICONTROL Sincronização de entidades do Dynamics]**.

  A sincronização deve ser desabilitada antes de sincronizar entidades personalizadas. Clique em **[!UICONTROL Esquema de sincronização]** se for sua primeira vez. Caso contrário, clique **[!UICONTROL Atualizar Esquema]**.

  ![Atualizar](assets/refreshSchema.png)

## Sincronizar o objeto personalizado

1. No lado direito, localize [!UICONTROL Lead], [!UICONTROL Contato]e [!UICONTROL Conta]objetos personalizados baseados em fontes.

   * **[!UICONTROL Ativar sincronização]** para os objetos em Lead se desejar acionar quando um Lead for adicionado a um contrato no Dynamics.

   * **[!UICONTROL Ativar sincronização]** para os objetos em Contato, se você deseja acionar quando um Contato é adicionado a um contrato no Dynamics.

   * **[!UICONTROL Ativar sincronização]** para os objetos em Conta, se você deseja acionar quando uma Conta é adicionada a um contrato no Dynamics.

   * **Ativar sincronização** para o objeto Contrato na página principal desejada (Cliente potencial, Contato ou Conta).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. Na nova janela, selecione as propriedades que deseja em Contrato.

   Ative as caixas em **[!UICONTROL Restrição]** e **[!UICONTROL Acionador]** para expô-los às suas atividades de marketing.

   ![Sincronização personalizada 1](assets/entitySync1.png)

   ![Sincronização personalizada 2](assets/entitySync2.png)

1. Reative a sincronização depois de habilitar a sincronização nos objetos personalizados.

   Voltar para a página [!UICONTROL Terminal de administração]e clique em **[!UICONTROL Microsoft Dynamics]** e clique em **[!UICONTROL Ativar sincronização]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Ativar global](assets/enableGlobalDynamics.png)

## Criar o programa

1. Entrada [!UICONTROL Atividades de marketing], clique com o botão direito **[!UICONTROL Atividades de marketing]** na barra esquerda, selecione **[!UICONTROL Nova Pasta de Campanha]** e nomeie-o.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito na pasta criada, selecione **[!UICONTROL Novo programa]** e dê um nome a ele.

   Deixe todo o resto como padrão e clique em **[!UICONTROL Criar]**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo programa 2](assets/newProgram2.png)

## Configurar [!DNL Twilio] SMS

Primeiro, verifique se você tem um [!DNL Twilio] e adquiriu os recursos de SMS necessários.

Configuração do Marketo - [!DNL Twilio] O webhook SMS requer três [!DNL Twilio] parâmetros da sua conta.

* SID da conta
* Token da conta
* Número de telefone do Twilio

Recupere esses parâmetros de sua conta e abra sua instância do Marketo.

1. Clique em **[!UICONTROL Admin]** no canto superior direito.

   ![Admin](assets/adminTab.png)

1. Clique em **[!UICONTROL Webhooks]** e clique em **[!UICONTROL Novo webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **[!UICONTROL Nome do webhook]** e **[!UICONTROL Descrição]**.

1. Insira o seguinte URL e substitua o `ACCOUNT_SID` e `AUTH_TOKEN` com o seu [!DNL Twilio] credenciais.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecionar **[!UICONTROL POST]** como seu tipo de Solicitação.

1. Insira o seguinte **Modelo** e certifique-se de substituir `MY_TWILIO_NUMBER` com o seu [!DNL Twilio] número de telefone e `YOUR_MESSAGE` com uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina o **[!UICONTROL Codificação do token de solicitação]** até *Formulário/URL*.

1. Definir o tipo de Resposta como *JSON* depois clique em **[!UICONTROL Salvar]**.

## Configurar o acionador da campanha inteligente

1. Na seção Atividades de Marketing, clique com o botão direito do mouse no programa que você criou e selecione **[!UICONTROL Nova campanha inteligente]**.

   ![Campanha inteligente 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **[!UICONTROL Criar]**.

   ![Campanha inteligente 2](assets/smartCampaign3.png)

   Há vários acionadores disponíveis para uso na pasta Microsoft.

1. Clique e arraste **[!UICONTROL Adicionado ao contrato]** para a **[!UICONTROL Smart List]** e, em seguida, adicione as restrições que desejar ter no acionador.

   ![Adicionado ao contrato](assets/addedToAgreementDynamics.png)

## Configurar o fluxo de campanha inteligente

1. Clique no botão **[!UICONTROL Fluxo]** na guia [!UICONTROL Campanha inteligente].

   Procure e arraste o **Ligar para Webhook** siga para a tela e selecione o webhook que você criou na seção anterior.

   ![Ligar para Webhook](assets/callWebhook.png)

1. Sua campanha de aviso por SMS para clientes potenciais adicionados a um contrato está configurada.
>[!TIP]
>
>Este tutorial é parte do curso [Acelere os ciclos de vendas com o Acrobat Sign para Microsoft Dynamics e Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!