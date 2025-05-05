---
title: Atualizações importantes de produtos Acrobat DC para clientes ETLA
description: Saiba mais sobre as alterações importantes nos direitos da Acrobat DC incluídos nas ofertas do ETLA (Enterprise Term License Agreement) de agosto de 2020 a novembro de 2020
feature: Deploy
role: Admin
level: Intermediate
jira: KT-7269
thumbnail: KT-7269.jpg
exl-id: 1a8d3f7d-96a4-4811-b4e9-9c55287b92ea
source-git-commit: 4e6fbf91e96d26f9ee8f1105ad68738b9450a32d
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 2%

---

# Atualizações importantes de produtos da Acrobat DC para clientes do ETLA

O [!DNL Adobe Sign Individual] (também conhecido como Adobe Sign Pro) será desprovisionado de todos os direitos do Acrobat DC incluídos nas ofertas do ETLA (Enterprise Term License Agreement) somente a partir de agosto de 2020 e continuará até 20 de novembro de 2020. O [!DNL Adobe Sign Individual] não fornece funcionalidade de nível corporativo e deve ser substituído pelo Adobe Sign Enterprise para clientes corporativos. Isso inclui o Acrobat DC licenciado como um aplicativo autônomo e o Acrobat DC licenciado como parte do Creative Cloud para corporações — Todos os Apps.

O acesso ao [!DNL Adobe Sign Individual] está disponível no Acrobat por meio da ferramenta **Adobe Sign** ou da ferramenta **Fill &amp; Sign** ([Solicitar assinaturas](https://www.adobe.com/br/acrobat/online/request-signature.html){target="_blank"}).

Acesso de ![[!DNL Adobe Sign Individual] no Acrobat DC](../assets/Deploy_SignEntitle1.png)

Se você não atualizou o Acrobat DC para a versão mais recente, a ferramenta pode estar identificada como &quot;Send for Signature“.

## Por que estamos desprovisionando isso?

[Em outubro de 2018, lançamos um novo Acrobat DC](https://news.adobe.com/news/news-details/2018/Adobe-Redefines-What-Is-Possible-With-PDF-With-All-New-Acrobat-DC). Esta versão mais recente inclui novas ferramentas e funcionalidades para trabalhar melhor com PDF em dispositivos móveis, na Web e no desktop, além de novas ferramentas de colaboração. Como assinante do Acrobat DC, você já deve ter esses ótimos recursos disponíveis. Outra atualização importante que lançamos foi a solução de assinatura eletrônica Adobe Sign.

Antes da versão de outubro de 2018, os usuários do Acrobat DC podiam enviar documentos para assinatura eletrônica usando ferramentas no Acrobat denominadas &quot;Fill &amp; Sign&quot; (ou &quot;Adobe Sign&quot; ou &quot;Send for Signature“) que receberam o direito [!DNL Adobe Sign Individual].

Embora esta opção tenha fornecido uma ótima maneira de capturar assinaturas eletrônicas, estamos desprovisionando o [!DNL Adobe Sign Individual] porque ele não fornece a funcionalidade de nível corporativo disponível por meio do Adobe Sign Enterprise, como:

* Capacidade de gerenciar centralmente usuários que têm permissão para enviar contratos ou assinar
* Permitir que administradores gerenciem contratos enviados e usados em toda a organização
* Fornecer controles granulares para gerenciar assinaturas eletrônicas em toda a organização

Além disso, o Adobe Sign Enterprise oferece mais funcionalidades em comparação com o que estava disponível no direito [!DNL Adobe Sign Individual], incluindo, entre outros:

* Administração
   * Logon único
   * Delegação de conta
* Integrações
   * Integrações empresariais pré-criadas com Dropbox, Salesforce, Workday etc.
   * O Adobe Sign é a solução de assinatura eletrônica preferencial no portfólio corporativo do [Microsoft](https://acrobat.adobe.com/us/en/business/integrations/microsoft.html), incluindo Office 365, SharePoint, Dynamics, Teams e Flow
* Personalização e otimização
   * Autenticação de assinatura eletrônica aprimorada, verificação de identidade de signatário baseada em ID avançada, designer de fluxo de trabalho, suporte avançado a idiomas etc.

O Adobe Sign é a solução líder do setor reconhecida globalmente para captura de assinaturas em conformidade com a lei. O Adobe Sign foi desenvolvido desde o início para atender a todas as necessidades de assinatura eletrônica da sua organização, com ferramentas de TI amigáveis para garantir que você e seus usuários usem assinaturas eletrônicas que estejam em total conformidade com os vários regulamentos regionais e do setor sobre assinaturas eletrônicas. Visite [aqui](https://helpx.adobe.com/br/enterprise/using/adobe-sign-for-enterprise.html) para obter mais informações sobre como gerenciar o Sign pelo [Adobe Admin Console](https://helpx.adobe.com/br/enterprise/using/admin-console.html).

Entre em contato com seu Adobe para discutir como você pode continuar fornecendo recursos de assinatura eletrônica para sua organização por meio de nossa plataforma mais ampla de documentos digitais que inclui o Acrobat DC e o Adobe Sign Enterprise.

## Acesso a contratos existentes

Os usuários ainda poderão acessar contratos enviados antes desta ação por meio do Adobe Document Cloud fazendo logon com sua Adobe ID em https://documentcloud.adobe.com. Se este usuário estiver agendado para migração no Sign Enterprise, ele precisará seguir estas [instruções](https://helpx.adobe.com/br/sign/kb/how-to-download-signed-documents---adobe-sign.html).

## Experiência do Acrobat DC sem direito [!DNL Sign Individual]

Os usuários com direitos do Adobe Sign Enterprise poderão enviar contratos no Acrobat usando o Adobe Sign ou a ferramenta [!UICONTROL Fill &amp; Sign] (Solicitar assinaturas).
Os usuários que não possuem direitos do Adobe Sign Enterprise não poderão enviar novos contratos e receberão uma mensagem de erro. O gráfico abaixo descreve os possíveis resultados.

![Mensagem de erro para a experiência do Acrobat DC](../assets/Deploy_SignEntitle2.png)

## Experiência do Adobe Document Cloud na Web sem direito ao Sign Individual

Os usuários poderão fazer logon em https://documentcloud.adobe.com/ para acessar e baixar contratos enviados antes do desprovisionamento do direito individual da Adobe Sign.

![Mensagem de erro para a experiência na Web do Document Cloud](../assets/Deploy_SignEntitle3.png)

## Para obter mais informações, visite as páginas abaixo:

* [Faça logon na Adobe Document Cloud](https://helpx.adobe.com/br/document-cloud/help/sign-in.html)
* [Gerenciando arquivos (Onde estão meus arquivos?)](https://helpx.adobe.com/br/document-cloud/help/manage-files.html)
* [Usando o [!UICONTROL Customization Wizard do Acrobat] para configuração](https://www.adobe.com/br/devnet-docs/acrobatetk/tools/Wizard/WizardDC/index.html)
* [Visão geral do [!UICONTROL Admin Console]](https://helpx.adobe.com/br/enterprise/using/admin-console.html)
* [Gerenciando o Adobe Sign no [!UICONTROL Admin Console]](https://helpx.adobe.com/br/enterprise/using/adobe-sign-for-enterprise.html)

**Revisões** 20 de maio de 2020; publicação original - agosto de 2019
