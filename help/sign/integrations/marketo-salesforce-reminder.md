---
title: Enviar lembretes usando o Acrobat Sign para Salesforce e o Guia de configuração do Marketo
description: Saiba como enviar um lembrete de email da Marketo quando um contrato permanece não assinado após um período
feature: Integrations
role: Admin
solution: Acrobat Sign, Marketo, Document Cloud
level: Intermediate
topic: Integrations
jira: KT-7248
topic-revisit: Integrations
thumbnail: KT-7248.jpg
exl-id: 33aca2e0-2f27-4100-a16f-85ba652c17a3
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# Enviar lembretes usando o Acrobat Sign para Salesforce e o Guia de configuração do Marketo

Saiba como enviar um lembrete de email da Marketo quando um contrato permanece não assinado após um período de tempo. Essa integração usa o Acrobat Sign, o Acrobat Sign para Salesforce, o Marketo e a sincronização do Marketo e do Salesforce.

## Pré-requisitos

1. Instale o Marketo Salesforce Sync.

   Informações e o plug-in mais recente do Salesforce Sync estão disponíveis [aqui.](https://experienceleague.adobe.com/docs/marketo/using/product-docs/crm-sync/salesforce-sync/understanding-the-salesforce-sync.html)

1. Instale o Acrobat Sign para Salesforce.

   Informações sobre este plug-in estão disponíveisName [aqui.](https://helpx.adobe.com/ca/sign/using/salesforce-integration-installation-guide.html)

## Localizar o objeto personalizado

Quando as configurações do Marketo Salesforce Sync e do Acrobat Sign para Salesforce estiverem concluídas, várias novas opções serão exibidas no Marketo Admin Terminal.

![Admin](assets/adminTab.png)

![Sincronização de objeto](assets/salesforceAdmin.png)

1. Clique em **Esquema de sincronização** se for sua primeira vez. Caso contrário, clique **Atualizar Esquema**.

   ![Atualizar](assets/refreshSchema1.png)

1. Se a sincronização global estiver em execução, desative clicando em **Desativar sincronização global**.

   ![Desabilitar](assets/disableGlobal.png)

1. Clique em **Atualizar Esquema**.

   ![Atualizar 2](assets/refreshSchema2.png)

## Sincronizar o objeto personalizado

No lado direito, consulte Objetos personalizados baseados em Lead, Contato e Conta.

**Ativar sincronização** para os objetos em Lead se desejar enviar um lembrete quando um lead não tiver assinado um contrato no Salesforce.

**Ativar sincronização** para os objetos em Contato, se desejar enviar um lembrete quando um Contato não tiver assinado um contrato no Salesforce.

**Ativar sincronização** para os objetos em Conta, se você deseja enviar um lembrete quando uma Conta não tiver assinado um contrato no Salesforce.

1. **Ativar sincronização** para a **Contrato** objeto mostrado na página principal desejada (cliente potencial, contato ou conta). Faça isso para qualquer outro objeto personalizado que você gostaria de sincronizar.

   ![Objeto do contrato](assets/agreementObject.png)

1. Os seguintes ativos mostram como **Ativar sincronização**.

   ![Sincronização personalizada 1](assets/customObjectSync1.png)

   ![Sincronização personalizada 2](assets/customObjectSync2.png)

## Expor os campos de objeto personalizados a acionadores

1. Enquanto a sincronização global está desativada, selecione o objeto personalizado do contrato para o qual a sincronização foi habilitada e **Editar campos visíveis**.

1. Marque o campo “Nome do contrato” na coluna do acionador para exibi-lo aos acionadores de ação de campanha. Marque outros campos pelos quais deseja filtrar e **Salvar**.

   ![Editar campos visíveis 1](assets/editVisible1.png)

   ![Editar campos visíveis 2](assets/editVisible2.png)

1. Quando terminar de ativar a sincronização nos objetos personalizados e expor os valores de acionamento, lembre-se de reativar a sincronização:

   ![Ativar global](assets/enableGlobal.png)

## Criar o programa e o token

1. Na seção Atividades de marketing do Marketo, clique com o botão direito do mouse em **Atividades de marketing** na barra esquerda, selecione **Nova Pasta de Campanha** e dê um nome a ele.

   ![Nova pasta](assets/newFolder.png)

1. Clique com o botão direito na pasta criada, selecione **Novo programa** e dê um nome a ele. Deixe todo o resto como padrão e clique em **Criar**.

   ![Novo programa 1](assets/newProgram1.png)

   ![Novo programa 2](assets/newProgram2.png)

1. Clique em **Meus Tokens** e, em seguida, arraste  **Script de e-mail** sobre a tela.

   ![Script de e-mail](assets/emailScript.png)

1. Dê um nome a ele e clique em **Clique para editar**.

   ![Nomear e editar](assets/nameAndSave.png)

1. Expandir **Objetos personalizados** no lado direito, expanda a guia **Contrato** objeto. Localize e arraste Nome do contrato, Status do contrato, Data de assinatura e URL de assinatura para a tela.

1. Escreva um script Velocity usando esses tokens para exibir o URL de um contrato que fica sem assinatura por uma semana. Aqui está um exemplo que compara a data atual com a Data de Envio:

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

## Criar o lembrete e adicionar personalização

Os exemplos de personalização incluem: o nome do signatário, o nome do contrato, um link para o contrato etc.

1. Clique com o botão direito do mouse no programa que você criou e clique em **Novo ativo local** e selecione **E-mail**.

   ![Novo email](assets/createNewEmail.png)

1. Na nova guia, insira um **Nome** e **Descrição** para o email e selecione um modelo no seletor de modelos. Clique em **Criar**.

   ![Seletor de Modelos](assets/templatePicker.png)

1. Defina o **Do nome** e **Do endereço**.

   ![Email de lembrete](assets/reminderEmail.png)

1. Clique no corpo da mensagem para ativar o Editor. Clique no botão **Inserir token** encontre o token de URL do contrato personalizado que você criou e clique em **Inserir**. Conclua a personalização de seu email e clique em **Salvar**.

   ![Inserir token](assets/insertToken.png)

1. Visualize usando um perfil que tenha um contrato atribuído a ele. Você verá um link para o URL com o Nome do contrato como rótulo.

   ![Link de email](assets/emailLink.png)

## Configurar o filtro da Campanha inteligente

1. Clique com o botão direito do mouse no programa que você criou e clique em **Nova campanha inteligente**.

   ![Campanha inteligente 1](assets/smartCampaign1.png)

1. Dê um nome de sua escolha e clique em **Criar**.

   ![Campanha inteligente 2](assets/smartCampaign2.png)

1. Procure por e, em seguida, clique e arraste **Tem contrato** à Smart List.

   ![Tem contrato](assets/hasAgreement.png)

1. Os campos que você expôs ao acionador agora devem estar disponíveis em **Adicionar Restrição**. Selecionar **Status do contrato** e qualquer outro campo pelo qual você deseja filtrar. Para cada campo adicionado, defina os valores pelos quais filtrar. Nesse caso, ele só será acionado quando o **Status do contrato** está Enviado para assinatura e **Data de envio** está nos últimos 7 dias.

   ![Status do contrato](assets/agreementStatus.png)

   >[!NOTE]
   >
   > d um identificador exclusivo para as restrições, como **Nome do contrato**, se você quiser que esta campanha seja executada apenas para determinados contratos.

1. Confirme o público da campanha e veja quem se qualificará na guia Programação.

   ![Qualificadores](assets/qualifiers.png)

## Configurar o fluxo de campanha inteligente

Porque o filtro de campanha **Dias sem assinatura** foi usado, você pode usar uma recorrência agendada para a campanha.

1. Clique no botão **Fluxo** na Campanha inteligente. Procure e arraste o **Enviar email** vá para a tela e selecione o email de lembrete que você criou na seção anterior.

   ![Enviar email](assets/sendEmail.png)

1. Clique no botão **Agendar** na Campanha inteligente. Verifique se o fluxo de campanha é limitado a ser executado somente uma vez por pessoa no **Configurações inteligentes da campanha**. Depois, clique no botão **Agendar Recorrência** guia.

   ![Guia Programação](assets/scheduleTab.png)

1. Defina o **Agendar** em Diário, escolha um dia e hora de início e uma data de término para a campanha, se necessário.

   ![Configurações de programação](assets/scheduleSettings.png)

>[!TIP]
>
>Este tutorial é parte do curso [Acelere os ciclos de vendas com o Acrobat Sign para Salesforce e Marketo](https://experienceleague.adobe.com/?recommended=Sign-U-1-2021.1) que está disponível gratuitamente no Experience League!
