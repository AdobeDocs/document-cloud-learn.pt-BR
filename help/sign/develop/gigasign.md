---
title: Reúna documentos de grande volume usando o GigaSign
description: Gigasign permite enviar, coletar e rastrear documentos para assinatura para milhares de pessoas ao mesmo tempo
feature: Workflow
role: Developer
level: Intermediate
jira: KT-6626
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: ba9931920ab3bfb6ea38a92cac4a35da1d0295cd
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Reúna documentos de grande volume usando o GigaSign

Gigasign permite enviar, coletar e rastrear documentos para assinatura para milhares de pessoas ao mesmo tempo. Ele foi desenvolvido para comunicações de grande volume com seus funcionários e clientes — oferecendo suporte a até 2.500 destinatários a cada envio em massa. O GigaSign usa a API do Acrobat Sign para fornecer a mesma funcionalidade do MegaSign e inclui suporte a vários signatários, grupos de destinatários, funções de destinatários, nomes de contratos, cópia carbono e muito mais.

>[!IMPORTANT]
>
>O GigaSign não está mais sendo atualizado para a versão mais recente do Java ou Acrobat Sign e terá suporte limitado. Os recursos do GigaSign estão sendo adicionados ao produto na seção [Envio em massa](https://experienceleague.adobe.com/docs/document-cloud-learn/sign-learning-hub/admin-set-up/getting-started-admin/megasign.html?) funcionalidade. Use o Envio em massa para todos os casos de uso que não exijam explicitamente o uso do GigaSign.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Baixar e instalar o aplicativo GigaSign

[Baixar arquivo zip do GigaSign](https://acrobat.adobe.com/id/urn:aaid:sc:US:001cf62d-1cab-46c7-aa96-661ac8680206)

[Link de download do Java 1.8 (somente se necessário)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[Endereços IP para lista branca (somente se necessário)](https://helpx.adobe.com/br/sign/system-requirements.html#IPs){target="_blank"}

## Instruções básicas de configuração

1. Faça logon na sua conta da Acrobat Sign.

1. Clique em **[!UICONTROL Agrupar]** ou **[!UICONTROL Conta]**, o que estiver no topo.

1. Digite “Tokens de acesso” no campo de pesquisa no lado esquerdo da tela.

1. Pressione o ícone “+” no lado direito.

1. Crie uma chave com os escopos necessários (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Clique duas vezes na tecla que você criou e copie o texto COMPLETO (ele sai da tela para a direita, então certifique-se de obter tudo).

1. Abra o GigaSign.

1. Clique no botão **[!UICONTROL Configurações]** no canto superior direito.

1. Cole a chave de integração na primeira linha.

1. Insira o endereço de email da conta usada para criar essa chave na segunda linha.

1. Clique em **[!UICONTROL Enviar]**.
