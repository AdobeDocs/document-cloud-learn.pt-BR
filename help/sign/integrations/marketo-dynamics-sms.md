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
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Enviar notificações usando o Acrobat Sign para Microsoft Dynamics 365 e Marketo

Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para informar ao signatário que um contrato está a caminho usando o Acrobat Sign, o Acrobat Sign para Microsoft Dynamic, o Marketo e o Marketo Microsoft Dynamics Sync. Para enviar notificações do Marketo, primeiro você precisa comprar ou configurar um recurso de gerenciamento de SMS do Marketo. Esta apresentação usa o [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas há outras soluções de SMS da Marketo disponíveis.

## Pré-requisitos

1. Instale o Marketo Microsoft Dynamics Sync.

   Informações e o plug-in mais recente do Microsoft Dynamics Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html?lang=pt-BR)

1. Instale o Acrobat Sign para Microsoft Dynamics.

   Informações sobre este plug-in estão disponíveis [aqui.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Microsoft Dynamics Sync e do Acrobat Sign for Dynamics estiverem concluídas, duas novas opções serão exibidas no Marketo Admin Terminal.

![Administrador](assets/adminTerminal.png)

* Clique em **[!UICONTROL Sincronização de Entidades do Dynamics]**.

  A sincronização deve ser desabilitada antes de sincronizar entidades personalizadas. Clique em **[!UICONTROL Sincronizar Esquema]** se esta for a primeira vez. Caso contrário, clique em **[!UICONTROL Atualizar Esquema]**.

  ![Atualizar](assets/refreshSchema.png)

## Sincronizar o objeto personalizado

1. No lado direito, localize objetos personalizados baseados em [!UICONTROL Lead], [!UICONTROL Contato] e [!UICONTROL Conta].

   * **[!UICONTROL Habilite a sincronização]** dos objetos sob Lead se desejar acionar quando um Lead for adicionado a um contrato no Dynamics.

   * **[!UICONTROL Habilite a sincronização]** dos objetos em Contato se desejar disparar quando um Contato for adicionado a um contrato no Dynamics.

   * **[!UICONTROL Habilite a Sincronização]** para os objetos em Conta se desejar disparar quando uma Conta for adicionada a um contrato no Dynamics.

   * **Habilite a Sincronização** para o objeto Contrato no Pai desejado (Cliente Potencial, Contato ou Conta).

   ![Objetos Personalizados](assets/enableSyncDynamics.png)

1. Na nova janela, selecione as propriedades que deseja em Contrato.

   Habilite as caixas em **[!UICONTROL Restrição]** e **[!UICONTROL Acionador]** para exibi-las às suas Atividades de Marketing.

   ![Sincronização Personalizada 1](assets/entitySync1.png)

   ![Sincronização Personalizada 2](assets/entitySync2.png)

1. Reative a sincronização depois de habilitar a sincronização nos objetos personalizados.

   Volte para o [!UICONTROL Terminal de Administração], clique em **[!UICONTROL Microsoft Dynamics]** e em **[!UICONTROL Habilitar Sincronização]**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Habilitar Global](assets/enableGlobalDynamics.png)

## Criar o programa

1. Em [!UICONTROL Atividades de Marketing], clique com o botão direito do mouse em **[!UICONTROL Atividades de Marketing]** na barra esquerda, selecione **[!UICONTROL Nova Pasta de Campanhas]** e nomeie-a.

   ![Nova Pasta](assets/newFolder.png)

1. Clique com o botão direito na pasta criada, selecione **[!UICONTROL Novo Programa]** e dê um nome a ela.

   Deixe tudo como padrão e clique em **[!UICONTROL Criar]**.

   ![Novo Programa 1](assets/newProgram1.png)

   ![Novo Programa 2](assets/newProgram2.png)

## Configurar SMS do [!DNL Twilio]

Primeiro verifique se você tem uma conta ativa do [!DNL Twilio] e se adquiriu os recursos de SMS necessários.

Configurar o webhook SMS do Marketo - [!DNL Twilio] requer três parâmetros [!DNL Twilio] da sua conta.

* SID da conta
* Token da conta
* Número de telefone do Twilio

Recupere esses parâmetros de sua conta e abra sua instância do Marketo.

1. Clique em **[!UICONTROL Administrador]** no canto superior direito.

   ![Administrador](assets/adminTab.png)

1. Clique em **[!UICONTROL Webhooks]** e em **[!UICONTROL Novo Webhook]**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **[!UICONTROL Nome do webhook]** e uma **[!UICONTROL Descrição]**.

1. Insira a URL a seguir e substitua `ACCOUNT_SID` e `AUTH_TOKEN` por suas credenciais [!DNL Twilio].

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecione **[!UICONTROL POST]** como seu tipo de Solicitação.

1. Insira o **Modelo** a seguir e substitua `MY_TWILIO_NUMBER` pelo seu número de telefone [!DNL Twilio] e `YOUR_MESSAGE` por uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina a **[!UICONTROL Codificação de Token de Solicitação]** como *Formulário/URL*.

1. Defina o tipo de Resposta como *JSON* e clique em **[!UICONTROL Salvar]**.

## Configurar o acionador da campanha inteligente

1. Na seção Atividades de Marketing, clique com o botão direito no programa que você criou e selecione **[!UICONTROL Nova Campanha Inteligente]**.

   ![Campanha Inteligente 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **[!UICONTROL Criar]**.

   ![Campanha Inteligente 2](assets/smartCampaign3.png)

   Há vários acionadores disponíveis para uso na pasta Microsoft.

1. Clique e arraste **[!UICONTROL Adicionado ao Contrato]** para a **[!UICONTROL Smart List]** e adicione as restrições que desejar ter no gatilho.

   ![Adicionado ao contrato](assets/addedToAgreementDynamics.png)

## Configurar o fluxo de campanha inteligente

1. Clique na guia **[!UICONTROL Fluxo]** na [!UICONTROL Campanha Inteligente].

   Pesquise e arraste o fluxo **Chamar webhook** para a tela e selecione o webhook criado na seção anterior.

   ![Chamar Webhook](assets/callWebhook.png)

1. Sua campanha de aviso por SMS para clientes potenciais adicionados a um contrato está configurada.
