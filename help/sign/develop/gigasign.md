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
source-git-commit: 452299b2b786beab9df7a5019da4f3840d9cdec9
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 5%

---

# Reúna documentos de grande volume usando o GigaSign

Gigasign permite enviar, coletar e rastrear documentos para assinatura para milhares de pessoas ao mesmo tempo. Ele foi desenvolvido para comunicações de grande volume com seus funcionários e clientes — oferecendo suporte a até 2.500 destinatários a cada envio em massa. O GigaSign usa a API do Acrobat Sign para fornecer a mesma funcionalidade do MegaSign e inclui suporte a vários signatários, grupos de destinatários, funções de destinatários, nomes de contratos, cópia carbono e muito mais.

>[!VIDEO](https://video.tv.adobe.com/v/328113?quality=12&learn=on&hidetitle=true)

## Baixar e instalar o aplicativo GigaSign

[Baixar arquivo zip do GigaSign](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Link de download do Java 1.8 (somente se necessário)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target="_blank"}

[Endereços IP para lista branca (somente se necessário)](https://helpx.adobe.com/br/sign/system-requirements.html#IPs){target="_blank"}

## Instruções básicas de configuração

1. Faça logon em sua conta do Acrobat Sign.

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
