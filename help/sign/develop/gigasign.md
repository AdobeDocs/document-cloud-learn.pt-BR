---
title: Coletar documentos de alto volume usando o GigaSign
description: Gigasign permite enviar, coletar e monitorar documentos para assinatura para milhares de pessoas ao mesmo tempo
role: User, Admin
product: adobe sign
level: Intermediate
topic-revisit: Integrations
thumbnail: 328113.jpg
exl-id: a59eab61-fe61-45c6-8137-f074e1f2b3ed
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 5%

---

# Reunir documentos de grande volume usando o GigaSign

O Gigasign permite enviar, coletar e monitorar documentos para assinatura para milhares de pessoas ao mesmo tempo. Ele foi projetado para comunicações de alto volume com seus funcionários e clientes, oferecendo suporte a até 2.500 destinatários a cada envio em massa. O GigaSign usa a API do Acrobat Sign para fornecer a mesma funcionalidade do MegaSign e inclui suporte para vários signatários, grupos de destinatários, funções de destinatário, nomes de contrato, cópia carbono e muito mais.

>[!VIDEO](https://video.tv.adobe.com/v/328113?hidetitle=true)

## Baixe e instale o aplicativo GigaSign

[Baixe o arquivo zip do GigaSign](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:8975dbca-98d5-4e66-9164-d21163c91c7f)

[Link de download do Java 1.8 (somente se necessário)](https://www.oracle.com/java/technologies/javase/javase8-archive-downloads.html) {target=&quot;_blank&quot;}

[Endereços IP para lista branca (somente se necessário)](https://helpx.adobe.com/br/sign/system-requirements.html#IPs){target=&quot;_blank&quot;}

## Instruções básicas de configuração

1. Faça logon em sua conta do Acrobat Sign.

1. Clique em **[!UICONTROL Grupo]** ou **[!UICONTROL Conta]**, o que estiver no topo.

1. Digite &quot;Tokens de acesso&quot; no campo de pesquisa no lado esquerdo da tela.

1. Pressione o ícone &quot;+&quot; no lado direito.

1. Crie uma chave com os escopos necessários (User_Read, Agreement_Read, Agreement_Write, Agreement_Send, Library_Read).

1. Clique duas vezes na tecla que você criou e copie o texto COMPLETO (ele vai para fora da tela à direita para garantir que você tenha tudo).

1. Abra o GigaSign.

1. Clique no botão **[!UICONTROL Configurações]** na parte superior direita.

1. Cole a chave de integração na primeira linha.

1. Insira o endereço de email da conta usada para criar essa chave na segunda linha.

1. Clique em **[!UICONTROL Enviar]**.
