﻿# README**Painless** é uma aplicação que tem como objetivo principal tornar o processo de desenvolvimento de pequenos sites e outras aplicações menos doloroso e mais rápido.# Instalador do Painless (Painless/ Installer)O Painless/ Installer é o instalador do Painless.<br/>> Para mais informações [clique aqui](https://github.com/junioraluisio/painless-installer)##### Antes de começarAntes de utilizar o Painless certifique-se que os seguintes programas estejam instalados em seu computador:- Composer [[+ info](https://getcomposer.org/download/)];- NodeJs [[+ info](https://nodejs.org/en/download/)];- Gulp [[+ info](https://gulpjs.com/)];##### Instalando via ComposerPrimeiro, baixe o instalador do Painless via Composer:> _composer global require painless/installer_##### Adicionando ao $PATHInsira o caminho do arquivo binário do Painless no Path do seu sistema operacional, este arquivo deverá estar na pasta global do Composer. Geralmente fica em:##### Windows> _%APPDATA%\Composer\vendor\bin_##### MacOS> _$HOME/.composer/vendor/bin_##### GNU/ Linux Distributions> _$HOME/.composer/vendor/bin_# Iniciando um projeto#### Comando _painless_Após instalado, o comando "*painless*" será habilitado no seu terminal e este será capaz de criar uma nova instalação do Painless no diretório de sua escolha. Por exemplo, o comando:> *_painless site_*Cria um diretório chamado "*site*" contendo todos os arquivos necessários para o funcionamento do Painless.#### Primeiras açõesExecutado o comando de criação do diretório e cópia dos arquivos necessários do Painless, a primeira ação que você deverá tomar é abrir o terminal no diretório de sua aplicação e digitar o comando:> *_composer install_*e depois:> *_npm install_*Estes comandos farão que todas as dependências do Painless sejam instaladas.# Banco de dados### Bancos de dados compatíveis* MySQL### Instruções da tabelaTodas as instruções para a criação da classe são baseadas nas informações da tabela que está sendo transformada em classe vem do banco de dados. São utilizadas instruções SQL para a captura das informações.### Nomeando tabelasPara que tudo fique corretamente separado, as tabelas obrigatoriamente devem possuir um prefixo seguido de underline (_), o prefixo é visto como um grupo, ou seja, tabelas com mesmos prefixos são armazenadas juntas.Todas as classes geradas são criadas diretamente no diretório "_core/Entities_", e tudo fica dividido em sub-pastas com os nomes dos prefixos da tabela que está sendo atacada, por exemplo, para a tabela "_auth_users_" será criada dentro da pasta "_Entities_" um diretório com o nome "_Auth_" e dentro deste serão armazenadas as classes "_Users_" e "_UsersManager_".Todas as tabelas que iniciarem com o mesmo prefixo ficarão juntas no diretório, voltando no exemplo acima todas as tabelas que iniciarem com "*auth\_*" ficarão juntas no diretório "_Auth_".### Instruções do campoCada campo da tabela deve conter em seu comentário uma string JSon que contem as informações específicas para configurar cada atributo ou método correspondente ao campo. Se divide em um array com os seguinte campos:+ *name_msg* -> string com o nome do campo que será apresentado para interação com o usuário+ _*validate*_ -> string que informa os parâmetros para validação do campo, recebe os seguintes valores:    * **auto_increment**: valida campo com numeração automática;    * **date_automatic**: valida um campo onde a data é informada automaticamente pelo sistema, padrão _date('Y-m-d H:i:s')_;    * **fk**: valida um campo do tipo _foreng key_;    * **string**: valida um campo que contem apenas uma cadeia de caracteres;    * **integer**: valida campos que armazenam números inteiros;    * **float**: valida campos que armazenam números decimais;    * **flag**: os flags são campos especiais que utilizam o campo nome para gerar uma string sem acentos ou caracteres especiais;    * **cpf**: valida campos que armazenam CPFs;    * **email**: valida campos que armazenam Emails;    * **token_user**: valida campos que armazenam Tokens de usuários;    * **login**: valida campos que armazenam Login;    * **password**: valida campos que armazenam Passwords;* _*validate_ref*_ -> string que informa a qual campo a validação faz referência, a exemplo os campos de validação do tipo "**flag**", "**jwt**" ou "**token**", ele são gerados automaticamente pelos sistema com base nas funções "_flag()_", "_jwt()_" e "_token()_" respectivamente;* _*insert*_ -> valor booleano que informa se o campo estará disponível em páginas de inserção de registro;* _*update*_ -> valor booleano que informa se o campo estará disponível em páginas de alteração de registro;* _*comment*_ -> Armazena o comentário do campo.### Arquivos de interação com o banco de dadosOs arquivos de interação com o banco de dados ficam dentro do diretório "_api/*_" com as ações de INSERT, UPDATE, ENABLE e DISABLE.# Configurações iniciais### Preenchendo o arquivo de configuração .env#### Informações do banco de dados* **DB_CONNECTION**<br/>Tipo de conexão do banco de dados, no momento Painless só aceita MySQL.* **DB_HOST:**<br/>Endereço da conexão com o banco de dados.* **DB_PORT**<br/>Porta da conexão com o banco de dados.* **DB_NAME**<br/>Nome do banco de dados.* **DB_USER**<br/>Nome do usuário do banco de dados.* **DB_PASS**<br/>Senha do banco de dados#### Informações das pastas do template* **VIEW_PATH**<br/>Pasta onde ficam a views do sistema * **VIEW_CACHE**<br/>Pasta onde ficam os arquivos de cache das views do sistema#### Informações do Token* **JWT_ISSUER**<br/>Origem do token.* **JWT_AUDIENCE**<br/>Público reivindicado.* **JWT_ID**<br/>Entidade a quem o token pertence, normalmente o ID do usuário* **JWT_SECRET**<br/>Chave secreta.# InvokerInvoker estabelece as classes do instalador do Painless, além de prover um maker de arquivos padrões para um software RESTFul.### TerminalO Invoker possui um maker que permite ser executado via terminal para escrita de classes, actions, routes, middlewares, além de um arquivo index e htaccess padrões que permite a utilização do sistema de rotas do PHP Slim e o gerenciador de templates do Twig. ##### Sintaxe dos comandos>php invoker [actions | classes | routes | htaccess | index | middleware] [empty | table:<table_name> | name:<name>]_**Classes**_:> php invoker classes table:<table_name>_**Actions**_:> php invoker actions table:<table_name>_**Routes**_:> php invoker routes table:<table_name>  _**Middlewares**_> php invoker middleware name:<middleware_name>_**Arquivo .htaccess padrão**_:  > php invoker htaccess  _**Arquivo index.php padrão**_> php invoker index### Formação de um link DashboardOs links utilizam os verbos HTTP para identificar quais ações serão executadas.[**POST**]   - inserção de novos registros.  [**PUT**]    - atualização de registros com base em um ID.  [**PATCH**]  - alterar um registro para "habilitado" com base em um ID.  [**DELETE**] - alterar um registro para "desabilitado" com base em um ID.##### Modelo do link_http://[dominio]/[target]/[id|empty]_>_Para mais informações de formação de links para aplicativos RESTFul leia: [Using HTTP Methods for RESTful Services](http://www.restapitutorial.com/lessons/httpmethods.html)._# Utilizando o gerenciador de tarefas GulpO arquivo _gulpfile.js_ do Painless já vem com uma série de tarefas pré-escritas que visam facilitar a tarefa de desenvolvimento do frontend, são elas:# FrontendAs alterações no frontend de sua aplicação são otimizadas através do Gulp#### Arquivos de estilo (*.scss)O Painless utiliza SASS e está habilitado para ler e reescrever seus arquivos *.scss em *.css. Os arquivos devem ser colocados no diretório:> *_assets > sass_*Para reescrever os arquivos abra o terminal e execute o comando:> *_gulp sass cssmin_*#### Arquivos javascriptOs arquivos javascript (*.js) são unidos em apenas um e minimizados. Os arquivos devem ser colocados no diretório:> *_assets > js_* Para reescrever os arquivos abra o terminal e execute o comando:> *_gulp jshint uglify_*#### Arquivos htmlOs arquivos HTML são minimizados para evitar carga desnecessária no navegador e como o Painless trabalha com template Twig você pode gerá as views automaticamente. Os arquivos *.html devem ser colocados dentro do diretório:> assets > viewsPara reescrever os arquivos abra o terminal e execute o comando:> *_gulp htmlmin_*#### LivereloadSe você tiver a extensão Livereload instalada no navegador de sua preferência, para habilitá-lo e para que todas as tarefas descritas acima sejam executadas automaticamente à medida que vc altera seus arquivos, basta executar o comando:> gulpCom isto, o Painless irá executar todas as tarefas e deixar o seu navegador em estado de alerta para fazer as alterações e apresentá-las.