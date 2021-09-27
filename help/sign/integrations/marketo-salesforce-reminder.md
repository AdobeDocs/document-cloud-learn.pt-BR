---
title: Enviar lembretes usando o Adobe Sign para Salesforce e o Guia de configuração do Marketo
description: Saiba como enviar um lembrete por email da Marketo quando um contrato não for assinado após um período de tempo
role: Admin
product: adobe sign
solution: Adobe Sign, Marketo, Document Cloud
level: Intermediate
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: bc79bbde966c99bdf32231ff073b49cfc759d928
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Enviar lembretes usando o Adobe Sign para Salesforce e o Guia de configuração do Marketo

Saiba como enviar um lembrete por email da Marketo quando um contrato não for assinado após um período de tempo. Essa integração usa Adobe Sign, Adobe Sign para Salesforce, Marketo e o Marketo e Salesforce Sync.

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

## Sincronizar o objeto personalizado

No lado direito, consulte Objetos personalizados baseados em Lead, Contato e Conta.

**Ative** Syncfor the objects em Lead se quiser enviar um lembrete quando um Lead não tiver assinado um contrato no Salesforce.

**Ative** Sincronizar para os objetos em Contato se quiser enviar um lembrete quando um Contato não tiver assinado um contrato no Salesforce.

**Ative** Syncfor the objects em Account (Conta) se quiser enviar um lembrete quando uma conta não tiver assinado um contrato no Salesforce.

1. **Ative** Syncfor the  **** Agreement object (Sincronizar) mostrado no item Parent (Lead, Contact ou Account) desejado. Faça isso para todos os outros objetos personalizados que você deseja sincronizar.

   ![Objeto do contrato](assets/agreementObject.png)

1. Os seguintes ativos mostram como **Ativar sincronização**.

   ![Sincronização personalizada 1](assets/customObjectSync1.png)

   ![Sincronização personalizada 2](assets/customObjectSync2.png)

## Exponha os campos de objeto personalizados aos acionadores

1. Quando a Sincronização global estiver desativada, selecione o objeto personalizado do contrato para o qual você ativou a sincronização e, em seguida, **Editar campos visíveis**.

1. Marque o campo &quot;Nome do contrato&quot; na coluna do acionador para expô-lo aos Acionadores de ação da campanha. Verifique quaisquer outros campos pelos quais você deseja filtrar e, em seguida, **Salvar**.

   ![Editar campos visíveis 1](assets/editVisible1.png)

   ![Editar campos visíveis 2](assets/editVisible2.png)

1. Quando terminar de ativar a sincronização nos objetos personalizados e expor os valores do acionador, lembre-se de reativar a sincronização:

   ![Ativar global](assets/enableGlobal.png)

## Criar o programa e o token

1. Na seção Atividades de marketing da Marketo, clique com o botão direito do mouse em **Atividades de marketing** na barra esquerda, selecione **Nova pasta da campanha** e dê um nome a ela.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito do mouse na pasta criada, selecione **Novo programa** e dê um nome a ela. Deixe tudo o resto como padrão e clique em **Criar**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo Programa 2](assets/newProgram2.png)

1. Clique em **Meus Tokens** e arraste **Script de e-mail** sobre a tela.

   ![Script de email](assets/emailScript.png)

1. Dê um nome a ele e clique em **Clique para Editar**.

   ![Nome e Editar](assets/nameAndSave.png)

1. Expanda **Objetos Personalizados** no lado direito e, em seguida, expanda o objeto **Contrato**. Localize e arraste o Nome do contrato, Status do contrato, Data de assinatura e URL de assinatura para a tela.

1. Escreva um script Velocity usando esses tokens para exibir o URL do contrato de um contrato que não está assinado por uma semana. Este é um exemplo que compara a data atual à data de envio:

   ```
   #foreach($agreement in $echosign_dev1__SIGN_Agreement__cList)
       #if($agreement.echosign_dev1__Status__c == "Out for Signature")
           #set($todayCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$date.get('yyyy-MM-dd'))) )
           #set($dateSentCalObj = $date.toCalendar($date.toDate("yyyy-MM-dd",$agreement.echosign_dev1__DateSent__c)) )
           #set($dateDiff = ($todayCalObj.getTimeInMillis() - $dateSentCalObj.getTimeInMillis()) / 86400000 )
   
           #if($dateDiff >= 7)
               #set($agreementName = $agreement.Name)
               #set($agreementURL = $agreement.echosign_dev1__Signing_URL__c.substring(8))
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

1. Clique em **Salvar**.

## Crie o lembrete e adicione personalização

Exemplos de personalização incluem: o nome do signatário, o nome do contrato, um link para o contrato etc.

1. Clique com o botão direito do mouse no programa que você criou e clique em **Novo ativo local** e selecione **Email**.

   ![Novo email](assets/createNewEmail.png)

1. Na nova guia, digite um **Nome** e **Descrição** para o email e selecione um modelo no seletor de modelo. Clique em **Criar**.

   ![Seletor de modelos](assets/templatePicker.png)

1. Defina **Do nome** e **Do endereço**.

   ![Email do lembrete](assets/reminderEmail.png)

1. Clique no corpo da mensagem para ativar o Editor. Clique no botão **Inserir Token**, localize o token personalizado do URL do contrato criado e clique em **Inserir**. Conclua a personalização do email e clique em **Salvar**.

   ![Inserir token](assets/insertToken.png)

1. Visualizar usando um perfil que tenha um contrato atribuído a ele. Você deve ver um link para o URL com o Nome do contrato como o rótulo.

   ![Enviar email com link](assets/emailLink.png)

## Configurar o Filtro da Campanha Inteligente

1. Clique com o botão direito do mouse no programa que você criou e clique em **Nova Campanha Inteligente**.

   ![Campanha inteligente 1](assets/smartCampaign1.png)

1. Dê um nome de sua escolha e clique em **Criar**.

   ![Smart Campaign 2](assets/smartCampaign2.png)

1. Procure e, em seguida, clique e arraste **Tem contrato** para a Lista inteligente.

   ![Tem contrato](assets/hasAgreement.png)

1. Os campos expostos ao acionador agora devem estar disponíveis em **Adicionar restrição**. Selecione **Status do contrato** e quaisquer outros campos pelos quais você deseja filtrar. Para cada campo adicionado, defina os valores para filtrar. Nesse caso, ele só será acionado quando o **Status do contrato** estiver Enviado para assinatura e **Data de envio** tiver passado antes de 7 dias.

   ![Status do contrato](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d um identificador exclusivo para as restrições, como **Nome do contrato**, se desejar que esta campanha seja executada apenas para determinados contratos.

1. Confirme o público-alvo da campanha e veja quem se qualificará na guia Programação.

   ![Qualificadores](assets/qualifiers.png)

## Configurar o Fluxo de Campanha Inteligente

Como o filtro de campanha **Dias sem assinatura** foi usado, você pode usar uma repetição programada para a campanha.

1. Clique na guia **Fluxo** na Campanha inteligente. Procure e arraste o fluxo **Enviar email** para a tela e selecione o email de lembrete criado na seção anterior.

   ![Enviar email](assets/sendEmail.png)

1. Clique na guia **Programação** na Campanha inteligente. Certifique-se de que o fluxo da campanha esteja limitado a ser executado apenas uma vez por pessoa nas **Configurações da campanha inteligente**. Em seguida, clique na guia **Agendar recorrência**.

   ![Guia Programação](assets/scheduleTab.png)

1. Defina **Agenda** como Diário, escolha um dia e hora de início e uma data de término para a campanha, se necessário.

   ![Configurações de agendamento](assets/scheduleSettings.png)

>[!TIP]
>
>Este tutorial é parte do curso [Acelere os ciclos de vendas com o Adobe Sign para Salesforce e o Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!
