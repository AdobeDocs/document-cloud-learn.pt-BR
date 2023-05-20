---
title: Automação de documentos com o Acrobat Sign para Microsoft Power Platform
description: Saiba como ativar e usar os conectores do Acrobat Sign e do Adobe PDF Tools para o Microsoft Power Apps. Crie fluxos de trabalho que automatizam processos de aprovação e assinatura corporativos com rapidez e segurança, sem nenhum código
role: User, Developer
level: Intermediate
topic: Integrations
thumbnail: KT-7488.jpg
kt: 7488
exl-id: 4113bc3f-293c-44a8-94ab-e1dbac74caed
source-git-commit: e02b1250de94ec781e7984c6c146dbae993f5d31
workflow-type: tm+mt
source-wordcount: '2436'
ht-degree: 1%

---

# Automação de documentos com o Acrobat Sign para Microsoft Power Platform

Saiba como ativar e usar os conectores do Acrobat Sign e do Adobe PDF Tools para o Microsoft Power Apps. Crie fluxos de trabalho que automatizam os processos de aprovação e assinatura corporativos com rapidez e segurança, sem nenhum código. Há quatro partes deste tutorial prático descritas nos links abaixo:

<table style="table-layout:fixed">
<tr>
  <td>
    <a href="documentautomation.md#part1">
        <img alt="Parte 1: Armazenar o contrato assinado no SharePoint com o Acrobat Sign" src="assets/documentautomation/AutomationPart1_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part1"><strong>Parte 1: Armazenar o contrato assinado no SharePoint com o Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
    <a href="documentautomation.md#part2">
        <img alt="Parte 2: Processo automatizado de aprovação para obter assinaturas eletrônicas com o Acrobat Sign" src="assets/documentautomation/AutomationPart2_thumb.jpg" />
    </a>
    <div>
    <a href="documentautomation.md#part2"><strong>Parte 2: Processo automatizado de aprovação para obter assinaturas eletrônicas com o Acrobat Sign</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part3">
      <img alt="Parte 3: OCR de documento automatizado com ferramentas do Adobe PDF" src="assets/documentautomation/AutomationPart3_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part3"><strong>Parte 3: OCR de documento automatizado com ferramentas do Adobe PDF</strong></a>
    </div>
  </td>
  <td>
   <a href="documentautomation.md#part4">
      <img alt="Parte 4: Montagem automatizada de documentos com o Adobe PDF Tools" src="assets/documentautomation/AutomationPart4_thumb.jpg" />
   </a>
    <div>
    <a href="documentautomation.md#part4"><strong>Parte 4: Montagem automatizada de documentos com o Adobe PDF Tools</strong></a>
    </div>
  </td>
</tr>
</table>

## Pré-requisitos

* Familiaridade do Microsoft 365 e do Power Automate
* Conhecimento da Acrobat Sign
* Conta do Microsoft 365 com acesso ao SharePoint e ao Power Automate (básico para Acrobat Sign, premium para ferramentas do Adobe PDF)
* Conta de desenvolvedor da Acrobat Sign para corporações ou Acrobat Sign

**Exercícios 1 e 2**

* Conta da Acrobat Sign com acesso à API. Uma conta de desenvolvedor ou uma conta corporativa.
* Site do SharePoint acessível pelo Power Automate ao qual você tem permissões de edição. Recomenda-se acesso administrativo total.
* Exemplo de documento para a solicitação de aprovação de assinatura e assinatura.

**Exercícios 3 e 4**

Baixar materiais [aqui](https://github.com/benvanderberg/adobe-sign-pdftools-powerautomate-tutorial)

## Parte 1: Armazenar o contrato assinado no SharePoint com o Acrobat Sign {#part1}

Na primeira parte, você usará um modelo do Power Automate Flow para configurar um fluxo de trabalho automatizado que salvará todos os contratos assinados no site do SharePoint.

1. Navegue até Power Automate.
1. Procure Acrobat Sign.

   ![Captura de tela de navegação para o Power Automate](assets/documentautomation/automation_1.png)

1. Escolha **Salve um contrato concluído do Acrobat Sign na biblioteca da SharePoint**.

   ![Captura de tela da ação Salvar um contrato concluído do Acrobat Sign na biblioteca do SharePoint](assets/documentautomation/automation_2.png)

1. Revise a tela e configure as conexões necessárias. Ative a conexão Acrobat Sign.
1. Clique no ícone `+` símbolo.

   ![Captura de tela da conexão de fluxo do Acrobat Sign e do SharePoint](assets/documentautomation/automation_3.png)

1. Insira o email da conta da Acrobat Sign e clique no campo de senha na nova janela.

   ![Captura de tela da tela de logon do Acrobat Sign](assets/documentautomation/automation_4.png)

   Aguarde um momento para que o Adobe verifique sua conta.

   >[!NOTE]
   >
   >Essa verificação o encaminhará para o logon apropriado se você estiver usando um Adobe ID ou nosso SSO corporativo.

1. Logon completo.
1. Clique em **Continuar** para ir para a tela Edição de fluxo.
1. Nomeie o acionador.

   ![Captura de tela de nomeação do acionador](assets/documentautomation/automation_5.png)

1. Defina suas configurações do SharePoint.

   ![Captura de tela de como definir as configurações do SharePoint](assets/documentautomation/automation_6.png)

   **Endereço do local:** Seu site da SharePoint
   **Caminho da Pasta:** Caminho para os Documentos Compartilhados que você deseja usar
   **Nome do arquivo:** Aceitar o padrão
   **Conteúdo do Arquivo:** Aceitar o padrão

1. Salve o fluxo.

   ![Captura de tela do ícone Salvar](assets/documentautomation/automation_7.png)

1. Navegue até a tela de visão geral do fluxo com a seta azul para trás. Você testará esse fluxo na parte 2.

   ![Captura de tela da tela de visão geral do fluxo](assets/documentautomation/automation_8.png)

Você testará esse fluxo na próxima parte.

## Parte 2: Processo automatizado de aprovação para obter assinaturas eletrônicas com o Acrobat Sign {#part2}

Na segunda parte, construímos a primeira parte com um fluxo mais robusto e testamos ambos os fluxos para vê-los em ação.

1. Selecionar **Modelos** no lado esquerdo da interface do Power Automate.

   ![Captura de tela da seleção de modelos](assets/documentautomation/automation_9.png)

1. Procure por &quot;aprovação do gerente&quot;.
1. Selecionar **Solicitar aprovação do gerente para um arquivo selecionado**.

   ![Captura de tela da seleção de aprovação do gerenciador de solicitações para um arquivo selecionado](assets/documentautomation/automation_10.png)

   Revise as conexões e adicione as que estiverem ausentes.

   >[!NOTE]
   >
   >Se este for o primeiro fluxo que você está fazendo com aprovações, elas serão completamente configuradas quando o fluxo for executado.

1. Clique em **Continuar** para ir para a tela de edição de fluxo.

   Esse fluxo tem muitas etapas pré-configuradas, incluindo verificação de erros e etapas condicionais aninhadas.

1. Configurar **Para um arquivo selecionado** do seguinte modo:
   **Endereço do local:** Seu site do SharePoint
   **Nome da biblioteca:** Seu repositório de documentos
1. Adicione uma entrada da seguinte maneira:
   **Tipo**: Email
   **Nome**: Email do signatário

   ![Captura de tela de configuração do fluxo](assets/documentautomation/automation_11.png)

1. Configurar **Obter propriedades do arquivo:** do seguinte modo:
   **Endereço do local:** Seu site do SharePoint
   **Nome da biblioteca:** Seu repositório de documentos

1. Role para baixo e procure **Em caso afirmativo**.

   ![Captura de tela da configuração Se sim](assets/documentautomation/automation_12.png)

1. Clique em **Adicionar uma ação** no **Em caso afirmativo** (não a mais inferior) para adicionar as etapas a serem enviadas para assinatura.

   ![Captura de tela da adição de uma ação na caixa Se sim](assets/documentautomation/automation_13.png)

1. Procurar **Conteúdo do arquivo de obtenção do SharePoint** e escolha **Obter conteúdo do arquivo**.

   ![Captura de tela da caixa de pesquisa](assets/documentautomation/automation_14.png)

1. Configure o **Obter conteúdo do arquivo** do seguinte modo:

   ![Captura de tela da configuração Obter conteúdo do arquivo](assets/documentautomation/automation_15.png)

   **Endereço do local:** Seu site da SharePoint.
   **Identificador de arquivo:** Procure por &quot;identificador&quot; e escolha Identificador na caixa **Obter propriedades do arquivo** etapa.
1. Procure por &quot;Adobe&quot; e escolha **Acrobat Sign** para adicionar outra ação.

   ![Captura de tela do menu de pesquisa](assets/documentautomation/automation_16.png)

1. Insira &quot;upload&quot; na caixa de pesquisa do Acrobat Sign e selecione **Fazer upload de um documento e obter uma ID de documento**.
1. Procurar a variável dinâmica **Nome** para obter o nome do item/documento selecionado no acionador sob **Nome do arquivo**.
1. Clique em **Expressão** no assistente variável em **Conteúdo do Arquivo**.

   ![Captura de tela da tela Fazer upload de um documento e obter uma ID de documento](assets/documentautomation/automation_17.png)

1. Adicione um único apóstrofo e clique em voltar para **Conteúdo dinâmico**, exclua seu apóstrofo, selecione **Conteúdo do Arquivo** e clique em **OK**.

   Verifique se não há apóstrofos adicionais e se parece com a amostra abaixo.

   ![Captura de tela da aparência que a tela Conteúdo dinâmico deve ter](assets/documentautomation/automation_18.png)

1. Procure por &quot;criar&quot; na área de pesquisa do Acrobat Sign para adicionar outra ação do Acrobat Sign.
1. Selecionar **Criar e assinar em um documento carregado e enviar para assinatura**.

   ![Captura de tela de pesquisa para criação](assets/documentautomation/automation_19.png)

1. Configure as informações necessárias: Escolha **Nome** no assistente de variável dinâmica em **Nome do contrato**.
Escolha **ID do documento** no assistente de variável dinâmica em **ID do documento**.
Escolha **Email do signatário** no assistente de variável dinâmica em **Email do participante**.
Digite &quot;1&quot; em **Pedido do participante**.
Escolha **Signatário** na lista suspensa em **Função do participante**.

   ![Captura de tela das informações necessárias](assets/documentautomation/automation_20.png)

1. **Salvar** o Flow.

### Teste o fluxo

Acesse o repositório de documentos do site do SharePoint para testá-lo.

1. Selecione o documento e escolha **Automatizar** e o **Fluxo** você acabou de criar.

   ![Captura de tela da seleção do menu e do fluxo Automatizar](assets/documentautomation/automation_21.png)

1. Inicie o fluxo para validar as conexões (somente a primeira execução do fluxo).
1. Insira uma boa mensagem para o aprovador em **Mensagem**.
1. Insira o email do signatário do documento em **Email do signatário**.
1. Clique em **Executar fluxo**.

O aprovador configurado para o usuário que inicia o fluxo receberá uma solicitação de aprovação. Você pode aprovar por email ou pelo menu Itens de ação do Power Automate.
Depois de aprovado, assine o documento. Dependendo do usuário e se ele estiver conectado ao Sign, talvez seja necessário abrir as janelas de assinatura em uma janela privada do navegador.

![Captura de tela de abertura em uma janela privada do navegador](assets/documentautomation/automation_22.png)

Conclua a assinatura e volte para a pasta do SharePoint.

![Captura de tela da pasta SharePoint](assets/documentautomation/automation_23.png)

## Parte 3: OCR de documento automatizado com ferramentas do Adobe PDF {#part3}

Na parte três, você aprenderá como automatizar o OCR em PDF quando eles forem importados para o Microsoft SharePoint. Isso resolve um problema que ocorre com documentos PDF digitalizados que não são pesquisáveis no SharePoint.

![Captura de tela do documento PDF no navegador](assets/documentautomation/automation_24.png)

### Configurar uma pasta no SharePoint

Acesse o Microsoft SharePoint onde deseja armazenar documentos.

1. Clique em **+ Novo** para criar uma nova pasta chamada &quot;Contratos Processados&quot;.
1. Clique em **+ Novo** para criar uma nova pasta chamada &quot;Contratos Antigos&quot;.

   ![Captura de tela de novas pastas](assets/documentautomation/automation_25.png)

Essas pastas agora são referenciadas como parte do seu fluxo do Power Automate.

### Criar um fluxo a partir de um modelo

1. Faça logon em https://flow.microsoft.com.
1. Clique em **Modelos** na barra lateral.

   ![Captura de tela de seleção de modelos](assets/documentautomation/automation_26.png)

1. Selecionar **Converter arquivos recém-adicionados em PDF de texto pesquisável no SharePoint**.
1. Clique no botão **+** símbolo ao lado de Adobe PDF Tools.

   ![Captura de tela da seleção do símbolo +](assets/documentautomation/automation_27.png)

1. Vá até https://www.adobe.com/go/powerautomate_getstarted em uma nova guia.
1. Clique em **Começar**.

   ![Captura de tela do botão Introdução](assets/documentautomation/automation_28.png)

1. Efetue login com seu Adobe ID.

   ![Captura de tela da tela Fazer logon](assets/documentautomation/automation_29.png)

1. Insira o Nome das credenciais e a Descrição das credenciais e clique em **Criar credenciais**.

   ![Captura de tela da tela Criar credenciais](assets/documentautomation/automation_30.png)

   Mantenha a janela com as credenciais abertas. Você precisará inseri-los no Microsoft Power Automate.

   ![Captura de tela da guia do navegador para manter aberta](assets/documentautomation/automation_31.png)

1. Insira as credenciais e clique em **Crie no Microsoft Power Automate**.

   ![Captura de tela de inserção das credenciais de Ferramentas PDF](assets/documentautomation/automation_32.png)

1. Clique em **Continuar**.

   ![Captura de tela de onde clicar em Continuar](assets/documentautomation/automation_33.png)

   Agora você pode ver uma exibição do fluxo de trabalho e precisará configurá-lo para o seu ambiente.

1. Selecione o campo Endereço do site e escolha o site do SharePoint que você está usando no acionador chamado **Quando um arquivo é criado em uma pasta**.

   ![Captura de tela de seleção Quando um arquivo é criado em um acionador de pasta](assets/documentautomation/automation_34.png)

1. Clique no ícone de pasta para navegar até a pasta Contratos antigos, localizada em ID da pasta.

   ![Captura de tela da seleção da pasta Contratos Antigos](assets/documentautomation/automation_35.png)

1. Edite o **Criar arquivo** ação na parte inferior do fluxo:

   Alterar **Endereço do site** para o endereço do site.
Especifique o local da pasta Contratos Processados no Caminho da Pasta.

1. Clique em **Salvar** no canto superior direito.
1. Clique em **Teste**.
1. Selecionar **Manualmente**.
1. Clique em **Teste**.

   ![Captura de tela do fluxo de teste](assets/documentautomation/automation_36.png)

### Experimente seu novo fluxo

1. Vá até a pasta Contratos antigos no SharePoint.
1. Navegue até E03/Old Contracts nos arquivos de exercícios baixados.
1. Copie os arquivos ReleaseFormXX.pdf na pasta Contratos Antigos no SharePoint.

   ![Captura de tela de cópia dos arquivos](assets/documentautomation/automation_37.png)

Agora, se você navegar até a pasta Contratos Processados , poderá ver suas PDF disponíveis após o fluxo ter alguns minutos para ser executado. Se você abrir os PDF, poderá ver que o texto pode ser selecionado.
Além disso, o SharePoint indexa o documento, permitindo pesquisar o conteúdo dos documentos na barra de pesquisa do SharePoint.

## Parte 4: Montagem automatizada de documentos com o Adobe PDF Tools {#part4}

Na parte quatro, você aprenderá a mesclar muitos documentos com base nas informações fornecidas ao selecionar e iniciar um fluxo do Microsoft SharePoint. Nesse cenário, o fluxo irá:

* Peça informações para escolher o que incluir em um pacote para um cliente.
* Com base nas informações fornecidas, ele mescla vários documentos. Esses documentos incluem uma folha de rosto e white papers opcionais.
* O documento mesclado é salvo no SharePoint.

### Importar arquivos de exercícios para o SharePoint

1. Abra a pasta E04 nos arquivos de exercícios.
1. Importe as pastas Proposta, Modelos e Documentos gerados no SharePoint.

   ![Captura de tela das pastas de importação](assets/documentautomation/automation_38.png)

Essas pastas serão usadas como referência. Em particular, você usará o arquivo Proposal.docx para sua proposta.

Na pasta Modelos, há uma pasta Capas que inclui designs de folhas de rosto para cidades diferentes. Há também uma pasta de white papers que contém white papers adicionais opcionais que serão anexados ao final, se selecionados.

### Importe o fluxo no Microsoft Power Automate

1. Faça logon no Microsoft Power Automate (https://flow.microsoft.com).
1. Clique em **Meus fluxos**.

   ![Captura de tela de onde selecionar Meus fluxos](assets/documentautomation/automation_39.png)

1. Clique em **Importar**.

   ![Captura de tela da tela de importação](assets/documentautomation/automation_40.png)

1. Clique em **Carregar** e escolha a pasta GenerateProposal_20210311231623.zip em E04/Flows/.

   ![Captura de tela da seleção da pasta](assets/documentautomation/automation_41.png)

1. Clique em **Importar**.

1. Clique no ícone de chave inglesa em Ação ao lado de **Enviar Proposta ao Cliente**.

   ![Captura de tela do ícone de chave inglesa](assets/documentautomation/automation_42.png)

1. Selecionar **Criar como novo** em Configuração.
1. Defina o nome do fluxo em Nome do Recurso.
1. Clique em **Salvar**.

   Repita isso para os outros recursos relacionados e selecione sua conexão.

   ![Captura de tela de como salvar o arquivo](assets/documentautomation/automation_43.png)

1. Clique em **Importar** depois de ter feito todas as suas conexões.

### Definir como um arquivo selecionado

Agora que o fluxo é criado, faça o seguinte:

1. Clique em **Editar**.

   ![Captura de tela de onde selecionar editar](assets/documentautomation/automation_44.png)

1. Selecione o acionador **Para um arquivo selecionado**.

   Adicione seu site do SharePoint no Endereço do site.
Adicione sua biblioteca na biblioteca.

   ![Captura de tela do acionador concluído](assets/documentautomation/automation_45.png)

### Definir templateFolderPath

1. Clique na variável templateFolderPath.
1. Defina o caminho para onde a pasta Modelos está localizada dentro do site do SharePoint que você importou.

### Definir conteúdo do arquivo de obtenção de capa

1. Clique em **Capa** , que expande o Escopo.
1. Expandir **Capa: Obter Conteúdo do Arquivo**.

   Defina o Endereço do site para seu site do SharePoint.

   ![Captura de tela da capa expandida](assets/documentautomation/automation_46.png)



### Definir arquivo selecionado

1. Expanda o **Arquivo selecionado** ação de escopo.

   Altere o Endereço do site e o Nome da biblioteca para o site do SharePoint e a Biblioteca respectivamente em **Obter propriedades do arquivo**.
Altere o Endereço do site para o site da SharePoint em **Obter conteúdo do arquivo**.

   ![Captura de tela da ação expandida Arquivo selecionado](assets/documentautomation/automation_47.png)

### Definir white papers

1. Clique em **White papers** ação.
1. Expandir **Condição: Adicionar white paper**.

   ![Captura de tela da condição expandida Adicionar white paper](assets/documentautomation/automation_48.png)

1. Expandir **White paper 1: Obter conteúdo do arquivo usando caminho**.
Edite o Endereço de site para o site da SharePoint especificado.

Repita as mesmas etapas para **Condição: Adicionar white paper 2**.

### Definir Criar Arquivo

1. Expandir **Criar arquivo**.

   Edite o endereço do site e o caminho da pasta para o site do SharePoint e o caminho onde a pasta Documentos gerados está localizada.

1. Clique em **Salvar**.

### Teste seu fluxo

1. Vá até a pasta Proposta no SharePoint.
1. Selecione a pasta Proposal.docx .

   ![Captura de tela da seleção da pasta de propostas](assets/documentautomation/automation_49.png)

1. Selecione seu fluxo no menu **Automatizar** menu.

   ![Captura de tela de Seleção do menu Automatizar](assets/documentautomation/automation_50.png)

1. Clique em **Continuar** para iniciar o fluxo.

   ![Captura de tela de Selecionar o botão Continuar](assets/documentautomation/automation_51.png)

1. Escolha sua capa e os white papers que deseja anexar.
1. Clique em **Executar fluxo**.

   ![Captura de tela do botão Executar fluxo](assets/documentautomation/automation_52.png)

Navegue até a pasta Gerar documentos. Agora você deve ver seu arquivo PDF gerado.

![Captura de tela do diretório SharePoint com o novo arquivo PDF](assets/documentautomation/automation_53.png)

### Adicionar o Protect e outras ações ao fluxo

Agora que você criou um fluxo com êxito, editará o fluxo para criptografar o documento PDF com uma senha. Isso também explica como você pode utilizar outras ações.

1. Navegue de volta para o final do fluxo.
1. Clique no botão **+** símbolo entre **Mesclar PDF** e **Criar arquivo**.

   ![Captura de tela de onde selecionar + símbolo](assets/documentautomation/automation_54.png)

1. Selecionar **Adicionar uma ação**.
1. Procure por &quot;Adobe PDF Tools&quot;.

   ![Captura de tela de pesquisa por Adobe PDF](assets/documentautomation/automation_55.png)

1. Selecionar **PDF Protect da visualização**.
1. Use Dynamic Content para definir o campo Nome do arquivo como **Nome do Arquivo PDF do PDF de Mesclagem**.

   ![Captura de tela de conteúdo dinâmico](assets/documentautomation/automation_56.png)

   No acionador, há um campo Senha que faz parte do formulário de iniciação. Podemos usar isso aqui.

1. Procurar **Campo Senha** usando conteúdo dinâmico e coloque-o no campo Senha.

   ![Captura de tela de pesquisa por senha](assets/documentautomation/automation_57.png)

1. Usar conteúdo dinâmico para defini-lo como **Conteúdo de Arquivo PDF de PDF de Mesclagem** no campo Conteúdo do Arquivo.
1. Altere o **Criar arquivo** para obter o conteúdo do arquivo do Protect PDF em vez de Mesclar PDF.
1. Expandir **Criar arquivo**.
1. Limpe o campo Conteúdo do arquivo.
1. Usar conteúdo dinâmico para inserir **Conteúdo do Arquivo PDF** de **PDF Protect da visualização**.

### Teste seu fluxo

1. Vá até a pasta Proposta no SharePoint.
1. Selecione Proposal.docx.

   ![Captura de tela da seleção da pasta Proposta](assets/documentautomation/automation_58.png)

1. Selecionar **Automatizar** para escolher seu fluxo.

   ![Captura de tela da seleção de Automatizar no menu](assets/documentautomation/automation_59.png)

1. Clique em **Continuar** para iniciar o fluxo.

   ![Captura de tela da seleção de Continuar](assets/documentautomation/automation_60.png)

1. Escolha a Capa e os white papers que deseja anexar.
1. Defina o campo Senha para a Senha que deseja definir.
1. Clique em **Executar fluxo**.

   ![Captura de tela dos arquivos selecionados e botão Executar fluxo](assets/documentautomation/automation_61.png)

1. Navegue até a pasta Gerar documentos.
Você deve ver seu arquivo PDF gerado. Abra o arquivo PDF e ele solicitará que você insira sua senha PDF.

   ![Captura de tela do PDF gerado no diretório do SharePoint](assets/documentautomation/automation_62.png)
