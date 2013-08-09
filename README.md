# Customizando a Interface do Pentaho Business Analytics

## Introdução

Este documento fornece orientações e instruções para personalizar as interfaces de usuário no Pentaho Business Analytics. Para ser bem sucedido com este documento, você deve ter algum nível de experiência em localização, ou desenvolvimento web e/ou projeto, ou você deve ter acesso a desenvolvedores Front-Ends que são capazes de executar essas operações de forma competente.

## Customizando o Pentaho User Console

O Pentaho User Console é a interface Web padrão para o Pentaho Business Analytics Server, e inclui elementos interativos de Análises e Relatórios Pentaho. O Pentaho Enterprise Console é a estrutura central do framework, através do qual o seu Business Analytics Server é configurado e gerenciado. Você pode personalizar a interface do User Console ao editar seus arquivos de configuração, imagens e folhas de estilos CSS3 manualmente, e tanto o user Console e Enterprise Console pode ser traduzida para outras línguas através da substituição de pacotes de mensagens de texto simples.

### Resumo dos arquivos de personalização e configuração

> **Nota:** Pare o servidor de aplicação Pentaho antes de editar qualquer coisa dentro do arquivo Pentaho WAR.

#### MantleSettings.properties

**Localização:** /pentaho/server/biserver-ce/tomcat/webapps/pentaho/WEB-INF/lib/mantle-4.8.0-GA.jar

Este arquivo é armazenado no pacote JAR acima listado no Pentaho WAR. Você deve abrir o JAR com um utilitário de arquivo ZIP, em seguida, navegue até */org/pentaho/mantle/server/*. Não importa como você irá extrair e editar o arquivo, ele deve ser colocado de volta no JAR quando for modificado. É recomenda o uso **7-Zip** para este processo, use seu editor de códido preferido, em seguida, faça suas modificações no arquivo.

O arquivo MantleSettings.properties contém configurações para a barra de menu, barra de ferramentas principal, e o painel logotipo. Se você decidir desabilitar o menu ou barra de ferramentas, o painel logotipo também será desabilitado por causa de restrições de interface do usuário. Verifique as configurações no arquivo como **show-menu-bar=true**. Para mudar o comportamento, basta alterar de **true** para **false**.

#### MantleStyle.css

**Localização:** /pentaho/server/biserver-ce/tomcat/webapps/pentaho/mantle/MantleStyle.css

Esta é a folha de estilo CSS do Pentaho User Console. Ele herda alguns elementos do arquivo widgets.css no mesmo diretório, você pode precisar dele também.

> **Nota:** Modificar essa folha de estilo poderia ter um impacto grande sobre a interface do Pentaho User Console.

#### Folhas de estilo locais e globais dos Temas Onyx e Slate

> **Nota:** O tema Slate está incluído no Servidor Business Analytics, mas desabilitado por padrão, porque tem problemas de renderização no Internet Explorer. No entanto, você pode achar que é útil para fins de desenvolvimento e testes.

Esta é a folha de estilo principal e estrutural, para o tema **padrão** do Pentaho User Console (Onyx).

**Localização:** */pentaho-solutions/system/common-ui/resources/themes/onyx/globalOnyx.css*

Esta é a folha de estilo principal e estrutural, específico do tema alternativo para o Pentaho User Console (Slate).

**Localização:** */pentaho-solutions/system/common-ui/resources/themes/onyx/globalSlate.css*

Esta é a folha de estilo do tema padrão, para o Pentaho User Console (Onyx).

**Localização:** */pentaho/mantle/themes/onyx/mantleOnyx.css*

Esta é a folha de estilo do tema alternativo, para o console de usuário Pentaho (Slate).

**Localização:** */pentaho/mantle/themes/slate/mantleSlate.css*

#### Configurações do tema específico do Analyzer, Dashboard Designer, e Interactive Reporting

Esses diretórios contêm folhas de estilo para cada ferramenta cliente BA Server.

**Analyzer location:** */biserver-ce/pentaho-solutions/system/analyzer/styles/themes/*

**Interactive Reporting location:** */biserver-ce/pentaho-solutions/system/pentaho-interactive-reporting/resources/web/themes/*

**Dashboard Designer location:** */biserver-ce/pentaho-solutions/system/dashboards/themes/*

### Substituindo o conjundo de ícones padrão

Os ícones utilizados em todo o Pentaho User Console são consolidadas e armazenadas em arquivos PNG chamados **image bundles**. Esses arquivos só abrange uma única solicitação HTTP a partir do cliente, para o servidor e para todo o conjunto de imagens, poupando largura de banda e melhorando o desempenho. Os pacotes de imagem têm nomes aleatórios gerados com as extensões PNG e são armazenados no diretório /pentaho/server/biserver-ee/tomcat/webapps/pentaho/mantle. Um exemplo de uma imagem de nome do bundle provável é: **EAC2E33CD4B780B5A88A44308412F1CB.cache.png**.

Se você editar um pacote de imagem, você deve ter certeza de preservar a sua localização e tamanho. A aplicação Web Pentaho utiliza CSS para cortar a imagem e agrupar durante a execução, de modo que você deve respeitar o tamanho, posição e localização do que é atualmente lá. Devido a essas restrições, é recomendado que você não altere as imagens em si. Isso pode ser feito com as ferramentas mais modernas de design gráfico.

### Alterando o logotipo padrão

O logotipo Pentaho exibido no canto superior direito da Pentaho User Console pode ser substituído ou desativado de acordo com suas necessidades. Para desabilidar o logotipo, altere o arquivo **MantleSettings.properties** explicação acima.

O logotipo padrão é: */pentaho/server/biserver-ce/tomcat/webapps/pentaho/mantle/themes/onyx/images/logo.png*, o logotipo padrão Pentaho tem um fundo transparente. Se você quiser modificar ou substituir o logotipo, você deve manter o nome do arquivo e tamanho da imagem, que é 152x75 pixels.

Se você quiser alterar o tamanho do logotipo, você pode alterar a classe CSS **.puc-logo-spacer** em **mantleOnyx.css** para usar diferentes dimensões:

<pre>
.puc-logo-spacer {
	width: 152px;
	height: 75px;
}
</pre>

#### Alterando o link do logotipo padrão

Você pode fazer o logotipo ir para uma determinada URL quando clicado. Por padrão, o logotipo do Pentaho não vai para nenhuma URL, mas a funcionalidade para torná-la clicável está ponta. Você pode definir a URL do destino, através do **logoPanelWebsite** em */pentaho/mantle/messages/mantleMessages.properties*. Este arquivo de propriedades está dentro do Pentaho WAR, então você terá que parar o Servidor Business Analytics, antes de fazer qualquer modificação.

### Alterando o Background do Workspace

Você pode alterar a imagem de fundo que aparece no painel de conteúdo do Pentaho User Console, modificando ou substituindo o **bg_pentaho_default.png** no arquivo *pentaho/system/common-ui/resources/themes/<theme-name>/images*. 

## Personalizando e Desenvolvendo Temas para Pentaho User Console

A interface gráfica do Pentaho User Console é construído sobre um motor de temas inovadores, baseados em CSS3. As seções abaixo contêm conselhos para Designers e Front-Ends.

### Visão geral do tema

O tema baseado em CSS3 permite que você mude o visual de suas ferramentas do Business Analytics Server e adicione seus próprios temas. Pode ser feito através do trabalho com apenas alguns arquivos de configuração chaves.

As folhas de estilo que compõem o Pentaho User Console, o Dashboard Designer, Analyzer e Interactive Reporting são na sua maioria em um único local. Coletivamente, esses estilos e scripts compreendem o tema padrão do sistema **Onyx**. Este tema está localizado no diretório UI plugin em */pentaho/server/biserver-ce/pentaho-solutions/system/common-ui/resources/themes*.

Existem dois tipos de temas: do **sistema** e **local**. Temas do sistema fornecem estilos e scripts comuns que se aplicam a todo Business Analytics Server. Por exemplo, os botões são definidos no tema padrão do sistema Onyx. Temas locais são definidos para uma determinada área ou "contexto" do servidor de BI. Contextos incluem plugins do Servidor Business Analytics, bem como os nomes dos diretórios de nível superior no Pentaho WAR. Recursos para temas locais só terão efeito em sua área específica do servidor de BI.

Qualquer página mostrada pelo Business Analytics Server que inclui o **webcontext.js** terá automaticamente todos os JavaScript do tema ativo e CSS incluído. Por exemplo:

    <themes root-folder="style">
       <autumn display-name="Autumn" system="true">
        <file>autumnStyles.css</file>
        <file>autumnScripts.js</file>
       </autumn>
    </themes>

Quando o tema **Autumn** estiver ativo, é adicionado à página HTML:

    <script type="text/javascript" src="/pentaho/common-ui/themes/autumn/autumnStyles.js"></script>
    <link rel="stylesheet" type="text/css" href="/pentaho/common-ui/themes/autumn/autumnStyles.css"/>

Esta inserção de recursos faz com que seja possível alterar os temas sem ter que editar os principais documentos HTML. Você pode incluir vários arquivos JavaScript e CSS para o seu tema.

Você pode adicionar estilos locais de uma forma similar. A única exigência é que você deve dizer ao sistema que contexto você precisa carregar. Isto é feito através da adição **?context=myPlugin** em **webcontext.js** script **myPlugin** é o nome do seu plugin ou a pasta raiz do WAR:

    <script type=”text/javascript” src=”webContext.js?context=myPlugin”></script>

### Criando um Novo Tema

Na inicialização, o Business Analytics procura por **themes.xml** em cada arquivo, plugin e pasta de nível raiz no Pentaho WAR. Vários temas podem ser definidos num ficheiro themes.xml. O exemplo a seguir define um tema do sistema chamado Autumn.

    <themes root-folder="resources/themes">
        <autumn display-name=”Autumn” system="true">
         <file>autumnStyles.css</file>
         <file>autumnScripts.js</file>
        </autumn>
        <autumn display-name=”Autumn” system="true">
         <file>localAutumnStyles.css</file>
        </autumn>
    </themes>

Observe que a tag **<themes>** tem a **pasta de raiz**. O valor do atributo **root-folder** é o nome do diretório (em relação ao contexto da aplicação Web) onde os temas são armazenados. Para contextos baseados em WAR, isso é simplesmente um nome de diretório dentro do WAR. Por exemplo, se o tema está localizado na pasta */pentaho.war/accounting/*, os recursos serão carregados a partir de */pentaho.war/accounting/resources/themes/*.

Carregamento de plugin de recursos é diferente do que WAR-based, ele controla a forma como os recursos são mapeados para o URL. Se o arquivo de tema de cima foi localizado em um plugin chamado **accounting**, em seguida, os recursos seriam acessadas a partir da seguinte URL: */pentaho/context/accounting/resources/themes/*. Este tipo de mapeamento de recursos é mais comumente implementado em plugins Business Analytics Server por meio da tag **static-path**:

    <static-paths>
        <static-path url="/accounting/resources" localFolder="resources"/>
    </static-paths>

É mais fácil e rápido desenvolver um novo tema, baseando-se no tema padrão do Onyx. Cada estilo definido no arquivo **mainStyles.css** é usado em algum lugar do Business Analytics Server. Onyx também contém vários arquivos de script, como por exemplo JScrollPane, barra de rolagem do jQuery. Esses scripts substitui as barras de rolagem do navegador nativo com versões personalizáveis ​​DHTML.

### Definindo um Tema Padrão

O tema padrão do sistema é definido no arquivo de configuração */pentaho-solutions/system/pentaho.xml* através do **default-theme**. O Business Analytics Server vem com **onyx** como o tema padrão, alterando o valor para um outro nome de tema, irá definir o tema ativo padrão para todos os usuários do Pentaho User Console.

### Temas Switching PUC

Se você criou um tema alternativo e/ou um pacote de mensagens, você pode mudar no Menu **View** do Pentaho User Console.

> **Nota:** Você pode impedir os temas que aparecem neste menu, adicionando um **hidden="true"** no arquivo de propriedades.

Você pode especificar manualmente um tema para uma determinada página, incluindo um **theme=** e o parâmetro URL. Isso afetará apenas a página solicitada. A seguir irá realizar um **debug** no sistema e temas locais, se disponíveis:

<pre>
http://localhost:8080/pentaho/content/myPlugin/index.html?theme=debug
</pre>

Se o sistema ou tema de debug local não for encontrado, os recursos serão carregados para o tema ativo em seu lugar. Isso é particularmente útil quando tem testes de novos temas e para carregar versões de depuração de scripts e estilos.

Também é possível definir a variável de sessão **pentaho-user-theme** para o nome do tema desejado. Isso geralmente é feito em uma ação de start-up para ter temas por usuário em cenários multi-locação.

---------------------------------------------------------------------------------------------------------------

Traduzido e adaptado de:
[Pentaho InfoCenter](http://infocenter.pentaho.com/help/index.jsp "Pentaho InfoCenter")
