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
source-git-commit: 51d1a59999a7132cb6e47351cc39a93d9a38eaeb
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Enviar notificações usando o Acrobat Sign para [!DNL Salesforce] e [!DNL Marketo]

Saiba como enviar uma mensagem de texto, um email ou uma notificação por push para permitir que o signatário saiba que um contrato está a caminho usando o Acrobat Sign, o Acrobat Sign para Salesforce, o Marketo e a sincronização do Marketo Salesforce. Para enviar notificações do Marketo, primeiro você precisa comprar ou configurar um recurso de gerenciamento de SMS do Marketo. Esta apresentação usa o [Twilio SMS](https://launchpoint.marketo.com/twilio/twilio-sms-for-marketo/), mas há outras soluções de SMS da Marketo disponíveis.

## Pré-requisitos

1. Instale o Marketo Salesforce Sync.

   Informações e o plug-in mais recente para o Salesforce Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instale o Acrobat Sign para Salesforce.

   Informações sobre este plug-in estão disponíveis [aqui.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Salesforce Sync e do Acrobat Sign for Salesforce estiverem concluídas, várias novas opções serão exibidas no Marketo Admin Terminal.

![Administrador](assets/adminTab.png)

![Sincronização de objetos](assets/salesforceAdmin.png)

1. Clique em **Sincronizar Esquema** se esta for a primeira vez. Caso contrário, clique em **Atualizar Esquema**.

   ![Atualizar](assets/refreshSchema1.png)

1. Se a sincronização global estiver em execução, desabilite clicando em **Desabilitar sincronização global**.

   ![Desabilitar](assets/disableGlobal.png)

1. Clique em **Atualizar Esquema**.

   ![Atualizar 2](assets/refreshSchema2.png)

## Sincronizar os objetos personalizados

No lado direito, consulte Objetos personalizados baseados em Lead, Contato e Conta.

**Habilite a Sincronização** para os objetos sob Lead se desejar acionar quando um Lead for adicionado a um contrato no Salesforce.

**Habilite a Sincronização** para os objetos em Contato se desejar acionar quando um Contato for adicionado a um contrato no Salesforce.

**Habilite a Sincronização** para os objetos em Conta se desejar acionar quando uma Conta for adicionada a um contrato no Salesforce.

1. **Habilite a Sincronização** para os objetos personalizados mostrados na página principal desejada (Lead, Contato ou Conta).

   ![Objetos Personalizados](assets/customObjects.png)

1. Os seguintes ativos mostram como **Habilitar a sincronização**.

   ![Sincronização Personalizada 1](assets/customObjectSync1.png)

   ![Sincronização Personalizada 2](assets/customObjectSync2.png)

1. Quando terminar de ativar a sincronização nos Objetos personalizados, reative a sincronização.

   ![Habilitar Global](assets/enableGlobal.png)

## Criar o programa

1. Na seção Atividades de Marketing do Marketo, clique com o botão direito do mouse em **Atividades de Marketing** na barra esquerda, selecione **Nova Pasta de Campanhas** e dê um nome a ela.

   ![Nova Pasta](assets/newFolder.png)

1. Clique com o botão direito na pasta criada, selecione **Novo Programa** e dê um nome a ela. Deixe tudo como padrão e clique em **Criar**.

   ![Novo Programa 1](assets/newProgram1.png)

   ![Novo Programa 2](assets/newProgram2.png)

## Configurar o Twilio SMS

Primeiro, certifique-se de ter uma conta ativa do Twilio e adquirir os recursos de SMS necessários.

Configurar o webhook Marketo - Twilio SMS requer três parâmetros do Twilio de sua conta.

- SID da conta
- Token da conta
- Número de telefone do Twilio

Recupere esses parâmetros de sua conta e abra uma instância do Marketo.

1. Clique em **Administrador** no canto superior direito.

   ![Administrador](assets/adminTab.png)

1. Clique em **Webhooks** e depois em **Novo Webhook**.

   ![Webhooks](assets/webhooks.png)

1. Insira um **Nome do webhook** e uma **Descrição**.

1. Insira a URL a seguir e substitua o **[ACCOUNT_SID]** e o **[AUTH_TOKEN]** pelas credenciais do Twilio.

   ```
   https://[ACCOUNT_SID]:[AUTH_TOKEN]@API.TWILIO.COM/2010-04-01/ACCOUNTS/[ACCOUNT_SID]/Messages.json
   ```

1. Selecione **POST** como seu tipo de Solicitação.

1. Insira o **Modelo** a seguir e substitua **[MY_TWILIO_NUMBER]** pelo seu número de telefone do Twilio e **[YOUR_MESSAGE]** por uma mensagem de sua escolha.

   ```
   From=%2B1[MY_TWILIO_NUMBER]&To=%2B1{{lead.Mobile Phone Number:default=edit me}}&Body=[YOUR_MESSAGE]
   ```

1. Defina a codificação do token de solicitação como Formulário/URL.

1. Defina o tipo de Resposta como JSON e clique em **Salvar**.

## Configurar o acionador da campanha inteligente

1. Na seção Atividades de Marketing, clique com o botão direito no programa que você criou e selecione **Nova Campanha Inteligente**.

   ![Campanha Inteligente 1](assets/smartCampaign1.png)

1. Nomeie-o e clique em **Criar**.

   ![Campanha Inteligente 2](assets/smartCampaign3.png)

   Se a configuração da sincronização de objeto personalizado foi feita corretamente, você deve ver os seguintes acionadores disponíveis para uso na pasta Salesforce.

1. Clique e arraste Adicionado ao contrato para a Smart List. Adicione quaisquer restrições que você deseja ter no acionador.

   ![Adicionado ao Contrato 2](assets/addedToAgreement2.png)

## Configurar o fluxo de campanha inteligente

1. Clique na guia **Fluxo** da Campanha Inteligente. Pesquise e arraste o fluxo **Chamar webhook** para a tela e selecione o webhook criado na seção anterior.

   ![Chamar Webhook](assets/callWebhook.png)

1. Sua campanha de aviso por SMS para clientes potenciais adicionados a um contrato está configurada.
