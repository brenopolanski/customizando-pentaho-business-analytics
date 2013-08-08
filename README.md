# Customizando a Interface do Pentaho Business Analytics

## Introdução

Este documento fornece orientações e instruções para personalizar as interfaces de usuário no Pentaho Business Analytics. Para ser bem sucedido com este documento, você deve ter algum nível de experiência em localização, ou desenvolvimento web e/ou projeto, ou você deve ter acesso a desenvolvedores front-ends que são capazes de executar essas operações de forma competente.

## Pentaho Styling Console de Usuário

O Console do usuário Pentaho é a interface Web padrão para o Pentaho BA Server, e inclui elementos interativos de Análises e Relatórios Pentaho. O Pentaho Enterprise Console é a estrutura central do framework, através do qual o seu BA Server é configurado e gerenciado. Você pode personalizar a interface do Usuário do Console ao editar seus arquivos de configuração, gráficos e folhas de estilos CSS3 manualmente, e tanto o Console de usuário e Enterprise Console pode ser traduzida para outras línguas através da substituição de pacotes de mensagens de texto simples.

### Resumo dos arquivos de personalização e configuração

> **Nota:** Pare o servidor de aplicação Pentaho antes de editar qualquer coisa dentro do arquivo Pentaho WAR.

#### MantleSettings.properties

**Localização:** /pentaho/server/biserver-ee/tomcat/webapps/pentaho/WEB-INF/lib/mantle-4.8.0-GA.jar

Este arquivo é armazenado no arquivo JAR acima listados no WAR Pentaho. Você deve abrir o JAR com um utilitário de arquivo ZIP, em seguida, navegue até */org/pentaho/mantle/server/*. Não importa como você irá extrair e editar o arquivo, ele deve ser colocado de volta no JAR quando for modificado. Pentaho recomenda o uso **7-Zip** para este processo, use seu editor de códido preferido, em seguida, faça suas modificações no arquivo.

O arquivo MantleSettings.properties contém configurações para a barra de menu, barra de ferramentas principal, e o painel logotipo. Se você decidir desabilitar o menu ou barra de ferramentas, o painel logotipo também será desabilitado por causa de restrições de interface do usuário. Verifique as configurações no arquivo como **show-menu-bar=true**. Para mudar o comportamento, basta alterar de **true** para **false**.

#### MantleStyle.css

**Localização:** /pentaho/server/biserver-ee/tomcat/webapps/pentaho/mantle/MantleStyle.css

Esta é a folha de estilo CSS do Pentaho User Console. Ele herda alguns elementos do arquivo Widgets.css no mesmo diretório, você pode precisar dele também.

> **Nota:** Modificar esses estilos poderia ter um impacto grande sobre o Pentaho User Console.

#### Folhas de estilo locais e globais dos Temas Onyx e Slate

> **Nota:** O tema Slate está incluído no Servidor BA, mas desabilitado por padrão, porque tem problemas de renderização no Internet Explorer. No entanto, você pode achar que é útil para fins de desenvolvimento e testes.

**Localização:** /pentaho-solutions/system/common-ui/resources/themes/onyx/globalOnyx.css

Esta é a folha de estilo principal e estrutural, para o tema padrão do console de usuário Pentaho (Onyx).

**Localização:** /pentaho-solutions/system/common-ui/resources/themes/onyx/globalSlate.css

Esta é a folha de estilo principal e estrutural, específico do tema alternativo para o Console do usuário Pentaho (Slate).

**Localização:** /pentaho/mantle/themes/onyx/mantleOnyx.css

Esta é a folha de estilo do tema padrão, para o console de usuário Pentaho (Onyx).

**Localização:** /pentaho/mantle/themes/slate/mantleSlate.css

Esta é a folha de estilo do tema alternativo, para o console de usuário Pentaho (Onyx).

#### Configurações do tema específico do Analyzer, Dashboard Designer, and Interactive Reporting

Esses diretórios contêm folhas de estilo para cada ferramenta cliente BA Server.

**Analyzer location:** /biserver-ee/pentaho-solutions/system/analyzer/styles/themes/

**Interactive Reporting location:** /biserver-ee/pentaho-solutions/system/pentaho-inte**ractive-reporting/resources/web/themes/

**Dashboard Designer location:** /biserver-ee/pentaho-solutions/system/dashboards/themes/

### Substituindo o conjundo de ícones padrão

Os ícones utilizados em todo o Pentaho User Console são consolidadas e armazenadas em arquivos PNG chamados **image bundles**. Esses arquivos só abrange uma única solicitação HTTP a partir do cliente, para o servidor e para todo o conjunto de imagens, poupando largura de banda e melhorando o desempenho. Os pacotes de imagem têm nomes máquina gerados com as extensões PNG e são armazenados no diretório /pentaho/server/biserver-ee/tomcat/webapps/pentaho/mantle directory. Um exemplo de uma imagem de nome do bundle provável é: **EAC2E33CD4B780B5A88A44308412F1CB.cache.png**.

Se você editar um pacote de imagem, você deve ter certeza de preservar a sua localização e tamanho. A aplicação Web Pentaho utiliza CSS para cortar a imagem e agrupar durante a execução, de modo que você deve respeitar o tamanho, posição e localização do que é atualmente lá. Devido a essas restrições, Pentaho recomenda que você não altere as imagens em si. Isso pode ser feito com as ferramentas mais modernas de design gráfico.

### Alterando o logotipo padrão

O logotipo Pentaho exibido no canto superior direito da Pentaho User Console pode ser substituído ou desativado de acordo com suas necessidades. Para desabilidar o logotipo, altere o arquivo **MantleSettings.properties** explicação acima.

O logotipo padrão é: /pentaho/server/biserver-ee/tomcat/webapps/pentaho/mantle/themes/onyx/images/logo.png, o logotipo padrão Pentaho tem um fundo transparente. Se você quiser modificar ou substituir o logotipo, você deve manter o nome do arquivo e tamanho da imagem, que é 152x75 pixels.

Se você quiser alterar o tamanho do logotipo, você pode alterar a classe CSS **.puc-logo-spacer** em **mantleOnyx.css** para usar diferentes dimensões:

<pre>
.puc-logo-spacer {
.  width: 152px;
.	height: 75px;
}
</pre>
