---
title: Enviar lembretes usando o Acrobat Sign para Microsoft Dynamics 365 e Marketo
description: Saiba como enviar um lembrete de email quando um contrato permanece não assinado após um período
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
topic-revisit: Integrations
jira: KT-7250
thumbnail: KT-7250.jpg
exl-id: 5a97fade-18a3-448a-8504-efb9e38e9187
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# Enviar lembretes usando o Acrobat Sign para Microsoft Dynamics 365 e Marketo

Saiba como enviar um lembrete de email quando um contrato permanece não assinado após um período de tempo. Essa integração usa o Acrobat Sign, o Acrobat Sign para Microsoft Dynamics, o Marketo e o Marketo Microsoft Dynamics Sync.

## Pré-requisitos

1. Instale o Marketo Microsoft Dynamics Sync.

   Informações e o plug-in mais recente do Microsoft Dynamics Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/microsoft-dynamics/marketo-plugin-releases-for-microsoft-dynamics.html)

1. Instalar [Acrobat Sign para Microsoft Dynamics](https://appsource.microsoft.com/pt-br/product/dynamics-365/adobesign.f3b856fc-a427-4d47-ad4b-d5d1baba6f86).

   Informações sobre este plug-in estão disponíveisName [aqui.](https://helpx.adobe.com/ca/sign/using/microsoft-dynamics-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Microsoft Dynamics Sync e do Acrobat Sign for Dynamics estiverem concluídas, duas novas opções serão exibidas no Admin Terminal do Marketo.

![Admin](assets/adminTerminal.png)

1. Clique em **[!UICONTROL Sincronização de entidades do Dynamics]**.

   A sincronização deve ser desabilitada antes de sincronizar entidades personalizadas. Clique em **Esquema de sincronização** se for sua primeira vez. Caso contrário, clique **Atualizar Esquema**.

   ![Atualizar](assets/refreshSchema.png)

## Sincronizar o objeto personalizado

1. No lado direito, localize [!UICONTROL Lead], [!UICONTROL Contato]e [!UICONTROL Conta]objetos personalizados baseados em fontes.

   * **Ativar sincronização** para os objetos sob **[!UICONTROL Lead]** se desejar enviar um lembrete quando um [!UICONTROL Lead] não assinou um contrato no Dynamics.

   * **Ativar sincronização** para os objetos sob **[!UICONTROL Contato]** se desejar enviar um lembrete quando um [!UICONTROL Contato] não assinou um contrato no Dynamics.

   * **Ativar sincronização** para os objetos sob **[!UICONTROL Conta]** se desejar enviar um lembrete quando um [!UICONTROL Conta] não assinou um contrato no Dynamics.

   * **Ativar sincronização** para o objeto contrato sob o **[!UICONTROL Pai]** ([!UICONTROL Lead], [!UICONTROL Contato], ou [!UICONTROL Conta]).

   ![Objetos personalizados](assets/enableSyncDynamics.png)

1. Na nova janela, selecione as propriedades que deseja em Contrato e ative as caixas em **Restrição** e **Acionador** para expô-los às suas atividades de marketing.

   ![Sincronização personalizada 1](assets/entitySync1.png)

   ![Sincronização personalizada 2](assets/entitySync2.png)

1. Reative a sincronização depois de habilitar a sincronização nos objetos personalizados.

   Volte para o Admin Terminal e clique em **Microsoft Dynamics** e clique em **Ativar sincronização**.

   ![Microsoft Dynamics](assets/microsoftDynamics.png)

   ![Ativar global](assets/enableGlobalDynamics.png)

## Criar o programa e o token

1. Na seção Atividades de marketing do Marketo, clique com o botão direito do mouse em **Atividades de marketing** na barra esquerda.

   Selecionar **Nova Pasta de Campanha** e dê um nome a ele.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito na pasta criada, selecione **Novo programa** e dê um nome a ele.

   Deixe todo o resto como padrão e clique em **Criar**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo programa 2](assets/newProgram2.png)

1. Clique em **Meus Tokens** e, em seguida, arraste **Script de e-mail** sobre a tela.

   ![Script de e-mail](assets/emailScript.png)

1. Dê um nome a ele e clique em **Clique para editar**.

   ![Nomear e editar](assets/nameAndSave.png)

1. Expandir **[!UICONTROL Objetos personalizados]** no lado direito, expanda a guia **[!UICONTROL Contrato]** objeto.

   Localizar e arrastar [!UICONTROL Nome], status do contrato, Enviado em e URL do signatário atual na tela.

1. Escreva um script Velocity usando esses tokens para exibir o URL de um contrato que fica sem assinatura por uma semana. Veja um exemplo que compara a data atual com a data de Enviado em:

   ```
   #foreach($agreement in $adobe_agreementList)
       #if($agreement.adobe_esagreementstatus == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.adobe_datesent)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.adobe_name)
               #set($agreementURL = $agreement.adobe_currentsignerurl.substring(8))
               #break
           #else
           #end
       #else
       #end
   #end
   
   #if(${agreementName})
       <a href="https://${agreementURL}">${agreementName}</a>
   #else
       Please contact us. 
   #end
   ```

1. Clique em **[!UICONTROL Salvar]**.

## Criar o lembrete e adicionar personalização

Os exemplos de personalização incluem: o nome do signatário, o nome do contrato, um link para o contrato etc.

1. Clique com o botão direito do mouse no programa que você criou e clique em **[!UICONTROL Novo ativo local]** e selecione **[!UICONTROL E-mail]**.

   ![Novo email](assets/createNewEmail.png)

1. Na nova guia, insira um **[!UICONTROL Nome]** e **[!UICONTROL Descrição]** para o email e selecione um modelo no seletor de modelos.

   ![Seletor de Modelos](assets/templatePicker.png)

1. Clique em **[!UICONTROL Criar]**.

1. Defina o **[!UICONTROL Do nome]** e **[!UICONTROL Do endereço]**.

   ![Email de lembrete](assets/reminderEmail.png)

1. Clique no corpo da mensagem para ativar o Editor.

   Clique no botão **[!UICONTROL Inserir token]** encontre o token de URL do contrato personalizado que você criou e clique em **[!UICONTROL Inserir]**. Conclua a personalização de seu email e clique em **[!UICONTROL Salvar]**.

   ![Inserir token](assets/insertToken.png)

1. Visualize usando um perfil que tenha um contrato atribuído a ele.

   Você verá um link para o URL com o Nome do contrato como rótulo.

   ![Link de email](assets/emailLink.png)

## Configurar o filtro da Campanha inteligente

1. Clique com o botão direito do mouse no programa que você criou e clique em **[!UICONTROL Nova campanha inteligente]**.

   ![Campanha inteligente 1](assets/smartCampaign1.png)

1. Dê um nome de sua escolha e clique em **[!UICONTROL Criar]**.

   ![Campanha inteligente 2](assets/smartCampaign2.png)

1. Procure por e, em seguida, clique e arraste **[!UICONTROL Tem contrato]** à Smart List.

   ![Tem contrato](assets/hasAgreementDynamics1.png)

   Os campos que você expôs ao acionador devem estar disponíveis em **[!UICONTROL Adicionar Restrição]**.

1. Selecionar **[!UICONTROL Status do contrato]** e qualquer outro campo pelo qual você deseja filtrar.

   Para cada campo adicionado, defina os valores pelos quais filtrar. Nesse caso, ele só é acionado quando a **[!UICONTROL Status do contrato]** é *Enviado para assinatura* e **[!UICONTROL Enviado em]** é *no passado antes de 1 semana*.

   ![Status do contrato](assets/hasAgreementDynaSentOn.png)

   >[!NOTE]
   >
   > Adicionar um identificador exclusivo às restrições, como **Nome**, se você quiser que esta campanha seja executada apenas para determinados contratos.

1. Confirme o público da campanha e veja quem se qualificará na guia Programação.

   ![Qualificadores](assets/qualifiers.png)

## Configurar o fluxo de campanha inteligente

Porque o filtro de campanha **Dias até a expiração** foi usado, você pode usar uma recorrência agendada para a campanha.

1. Clique no botão **[!UICONTROL Fluxo]** na guia [!UICONTROL Campanha inteligente].

   Procure e arraste o **Enviar email** vá para a tela e selecione o email de lembrete que você criou na seção anterior.

   ![Enviar email](assets/sendEmail.png)

1. Clique no botão **[!UICONTROL Agendar]** na Campanha inteligente. Verifique se o fluxo de campanha é limitado a ser executado somente uma vez por pessoa no **Configurações inteligentes da campanha**. Depois, clique no botão **Agendar Recorrência** guia.

   ![Guia Programação](assets/scheduleTab.png)

1. Defina o **Agendar** até _Diariamente_. Escolha um dia e hora de início e uma data de término para a campanha, se necessário.

   ![Configurações de programação](assets/scheduleSettings.png)

>[!TIP]
>
>Este tutorial é parte do curso [Acelere os ciclos de vendas com o Acrobat Sign para Microsoft Dynamics e Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!