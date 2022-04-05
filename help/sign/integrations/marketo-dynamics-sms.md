---
title: Enviar notificações usando o Acrobat Sign para Microsoft Dynamics 365 e Marketo
description: Saiba como enviar uma mensagem de texto, email ou notificação por push para permitir que o signatário saiba que um contrato está a caminho
role: Admin
product: adobe sign
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7249.jpg
exl-id: 2e0de48c-70bf-4dc5-8251-88e7399f588a
source-git-commit: 60582eeaf8437ca1206f45b0b6daf96629c16b61
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Enviar notificações usando o Adobe Sign para Microsoft Dynamics 365 e Marketo

Saiba como enviar uma mensagem de texto, email ou notificação por push para permitir que o signatário saiba que um contrato está a caminho usando o Adobe Sign, o Adobe Sign para Microsoft Dynamic, o Marketo e o Marketo Microsoft Dynamics Sync. Para enviar notificações do Marketo, primeiro você precisa comprar ou configurar um recurso de gerenciamento de SMS do Marketo. Este passo a passo usa [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas outras soluções de SMS da Marketo estão disponíveis.

## Pré-requisitos

1. Instale o Marketo Microsoft Dynamics Sync.

   Informações e o plug-in mais recente do Microsoft Dynamics Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instale o Adobe Sign para Microsoft Dynamics.

   Informações sobre este plug-in estão disponíveis [aqui.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Microsoft Dynamics Sync e do Adobe Sign for Dynamics estiverem concluídas, duas novas opções serão exibidas no Marketo Admin Terminal.

![Admin.](assets/adminTerminal.png)

* Clique em **[!UICONTROL Sincronização de Entidades do Dynamics]**.

   A sincronização deve ser desabilitada antes da sincronização de entidades personalizadas. Clique em **[!UICONTROL Esquema de sincronização]** se esta é a sua primeira vez. Caso contrário, clique em **[!UICONTROL Atualizar Esquema]**.

   ![Atualizar](assets/refreshSchema.png)

## Sincronizar o objeto personalizado

1. No lado direito, localize [!UICONTROL Lead], [!UICONTROL Contato]e [!UICONTROL Conta]objetos personalizados baseados em código.

   * **[!UICONTROL Ativar sincronização]** para os objetos em Lead, se desejar acionar quando um Lead for adicionado a um contrato no Dynamics.

   * **[!UICONTROL Ativar sincronização]** para os objetos em Contato, se desejar acionar quando um Contato for adicionado a um contrato no Dynamics.

   * **[!UICONTROL Ativar sincronização]** para os objetos em Conta, se você deseja acionar quando uma Conta é adicionada a um contrato no Dynamics.

   * **Ativar sincronização** para o objeto Contrato sob o Pai desejado (Lead, Contato ou Conta).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. Na nova janela, selecione as propriedades desejadas em Contrato.

   Ative as caixas em **[!UICONTROL Restrição]** e **[!UICONTROL Acionador]** para exibi-las às suas atividades de marketing.

   ![Sincronização personalizada 1](assets/entitySync1.png)

   ![Sincronização personalizada 2](assets/entitySync2.png)

1. Reative a sincronização depois de habilitar a sincronização nos objetos personalizados.

   Volte para a página [!UICONTROL Terminal do administrador]e clique em **[!UICONTROL Microsoft Dynamics]** e clique em **[!UICONTROL Ativar sincronização]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Ativar Global](assets/enableGlobalDynamics.png)

## Criar o programa

1. No [!UICONTROL Atividades de marketing], clique com o botão direito do mouse **[!UICONTROL Atividades de marketing]** na barra esquerda, selecione **[!UICONTROL Nova Pasta de Campanha]** e dê um nome a ela.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito do mouse na pasta criada e selecione **[!UICONTROL Novo programa]** e dê um nome.

   Deixe todo o resto como padrão e clique em **[!UICONTROL Criar]**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo programa 2](assets/newProgram2.png)

## Configurar [!DNL Twilio] SMS

Primeiro, verifique se você tem um [!DNL Twilio] conta e comprou os recursos de SMS que você precisa.

Configuração do Marketo - [!DNL Twilio] O webhook do SMS requer três [!DNL Twilio] parâmetros da sua conta.

* SID da conta
* Token da conta
* Número de telefone do Twilio

Recupere esses parâmetros da sua conta, agora abra sua instância do Marketo.

1. Clique em **[!UICONTROL Admin]** no canto superior direito.

   ![Admin.](assets/adminTab.png)

1. Clique em **[!UICONTROL Webhooks]** e clique em **[!UICONTROL Novo webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **[!UICONTROL Nome do webhook]** e **[!UICONTROL Descrição]**.

1. Insira o seguinte URL e substitua o `ACCOUNT_SID` e `AUTH_TOKEN` com seu [!DNL Twilio] credenciais.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecionar **[!UICONTROL POST]** como seu tipo de Solicitação.

1. Insira o seguinte **Modelo** e certifique-se de substituir `MY_TWILIO_NUMBER` com seu [!DNL Twilio] número de telefone e `YOUR_MESSAGE` com uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina o **[!UICONTROL Codificação de Token de Solicitação]** para *Formulário/URL*.

1. Defina o tipo de resposta como *JSON* clique em **[!UICONTROL Salvar]**.

## Configurar o Gatilho da Campanha Inteligente

1. Na seção Atividades de marketing, clique com o botão direito do mouse no programa que você criou e selecione **[!UICONTROL Nova Campanha Inteligente]**.

   ![Smart Campaign 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **[!UICONTROL Criar]**.

   ![Smart Campaign 2](assets/smartCampaign3.png)

   Você deverá ver vários acionadores disponíveis para uso na pasta Microsoft.

1. Clique e arraste **[!UICONTROL Adicionado ao contrato]** ao **[!UICONTROL Smart List]** e adicione as restrições que deseja ter no acionador.

   ![Adicionado ao contrato](assets/addedToAgreementDynamics.png)

## Configurar o fluxo de campanha inteligente

1. Clique no botão **[!UICONTROL Fluxo]** na guia [!UICONTROL Campanha inteligente].

   Pesquise e arraste o **Chamar Webhook** vá para a tela e selecione o webhook criado na seção anterior.

   ![Chamar Webhook](assets/callWebhook.png)

1. Sua campanha de aviso por SMS para clientes potenciais adicionados a um contrato já foi configurada.
>[!TIP]
>
>Este tutorial faz parte do curso [Agilizar os ciclos de vendas com o Adobe Sign para Microsoft Dynamics e Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!