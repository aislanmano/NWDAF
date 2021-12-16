	1) Antes Instalar as ferramentas: Visual Code, NodeJS, GoLand, Net-tools, OpenSSH, MongoDB executar um "sudo apt-get update" para atualização de pacotes
	. Para verificar a versão de instalação do Visual Code, digitar: code --version
	. Para verificar a versão de instalação do Nodejs, digitar: nodejs --version
	
	. Goland: 
	  1. sudo apt-get install snapd
	  2. sudo snap install goland --classic
	. NetTools: sudo apt-get install net-tools
	. MongoDB: para verificar o MongoDB inicializar com o comando "Mongo" e para ver os databases instalado, executar o comando: "show databases"
	
	2) Criar um diretório
	. Exemplo: openapi_teste
	
	3) Instalar o Editor Texto
  Editores de linha de comando (CLI)
  . Openapi generator tech docs installation

	4) Procurar no google o Repositório que tenha a função e serviço do NWDAF
	4.1. site:github.com Nnwdaf_AnalyticsInfo.yaml
	. Depois de clicar em RAW, copiar tudo.	
	
  <img src="https://user-images.githubusercontent.com/29335033/146395128-dca01f3b-e59f-4219-96cc-00b118ada528.png"/>
  
  <img src="https://user-images.githubusercontent.com/29335033/146399991-9d99c705-ee4e-4aac-bb3f-310e38817239.png"/>
	
	
	--> Tem que ter permissão de leitura e escrita neste diretório (openapi_teste)
	. Chown Labora -R 
	
	5) Touch <nome do arquivo>  - para criar o nome do arquivo
	. Touch Nnwdaf_AnalyticsInfo.yaml
	. Verificar se o arquivo foi criado corretamente
	
	6) Abrir o Vidual Code e cola o códgio copiado do arquivo do GitHub:
  
  <img src="https://user-images.githubusercontent.com/29335033/146400504-71977d60-1a0f-44fb-9a9e-73794e42377b.png"/>
	
	. Este arquivo . YAML foi implementado de acordo com as prerrogativas doa openapi seguindo a especificação da 3gpp que descreve o micro serviço analytics Info para ser provido pela NWDAF.
	. Também outro serviço que é gerado sobre a sobrescrita de eventos
	
	7) Criar um diretório chamado "Deploy"
  <img src="https://user-images.githubusercontent.com/29335033/146400800-985f0a3f-4cd1-4233-9b67-c12389c9c63d.png"/>
  	
	8) Em seguida abrir o Terminal pelo próprio Visual Code
  <img src="https://user-images.githubusercontent.com/29335033/146400978-9436b594-ca77-4d96-97fd-0cc45b57989e.png"/>
  	
	
	9) Em seguida aplicar as prerrogativas da máquina com o comando 
	 . sudo su
  <img src="https://user-images.githubusercontent.com/29335033/146401113-08c53d5c-8d0f-43b8-a621-a6dd88d01953.png"/>	
  
	10) Acessar o diretorio "deploy" em seguida mover o arquivo "TS29520_Nnwdaf_AnalyticsInfo.yaml" para dentro deste diretório
  <img src="https://user-images.githubusercontent.com/29335033/146401222-9fee119a-b572-407d-9e0d-6a538698b4a6.png"/>
  
	11) seguida, executar o comando para fazer a leitura do código .YAML com o CLI que foi instalado anteriormente gera e faça a construção dos "scafolds" em código fonte.
	. sudo openapi-generator-cli generate -i TS29520_Nnwdaf_AnalyticsInfo.yaml -g go --skip-validate-spec -o api/Nnwdaf_AnalyticsInfo/
  <img src="https://user-images.githubusercontent.com/29335033/146401300-a06d0173-0a59-4974-b688-22eff5ae3b8e.png"/>
  	
	12) O mecanismo do opeapi fez todo mecanismo do arquivo .yaml e dentro da pasta Deploy esta criado com sucesso:
  <img src="https://user-images.githubusercontent.com/29335033/146401463-a7e1b90e-f500-47d9-a5c6-ef411e2a54f8.png"/>
  	
	13) Dentro da pasta Deploy possui a pasta api
	. Nesta pasta tem diversos arquivos .go
	. Tudo isto com as devidas dependências, com a estrutura de conexão com as apis,  com os endpoints determinados lá na especificações, todos esses arquivos .go e as subpastas dentro de api foram gerados e construído através daquele arquivo .yaml. Aqui já possui too o scafuld inicial necessário para começar a trabalhar e construir a implementação de AnalyticsInfo. Estão tudo estruturado para começar a implementar a api
	- O ideal seria pegar a espeficição e fazer um de_para dessas especificações.
	
	. Assim foi gerado o código GO a partir dos .YML que especificam a NWDAF, fazendo uso de um CLI para gerar código a partir de especificações do arquivo .YML
	
	14) Implementar o núcleo free5gc, implementar esta ambiente de desenvolvimento em modo depuração com uma versão da NWDAF (que esta em construção) que coleta ANF.
	15) Fazer um forke/baixar o free5gc do github com o comando:
	. git clone --recursive -b master -j `nproc` https://github.com/ciromacedo/free5gc.git
	

	16) Em seguida abri o GoLand e apontar para a pasta do projeto "free5gc"
  <img src="https://user-images.githubusercontent.com/29335033/146401569-64a132c5-ade9-4c99-8337-a0ea375e0226.png"/>
  
	
	17) Inicializar o free5gc
  <img src="https://user-images.githubusercontent.com/29335033/146401779-ffd9a368-3b15-4155-98d2-63d7b5750ffc.png"/>
  
	18) Configurando o goland com freegc para fazer o Debug
	https://www.free5gc.org/installations/stage-3-free5gc-install/
