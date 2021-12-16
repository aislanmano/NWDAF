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
  	
	17) Deve instalar o SDK no Go Land
  <img src="https://user-images.githubusercontent.com/29335033/146401779-ffd9a368-3b15-4155-98d2-63d7b5750ffc.png"/>
  
	. Aguardar fazer o download e depoi clicar no botão OK, onde deve iniciar a instalação e configuração:
  <img src="https://user-images.githubusercontent.com/29335033/146402093-ee2f0f24-21e0-4cdf-bbb4-c3d7ac881bec.png"/>
  
	. Veja na imagem abaixo que foi instalado o SDK na ferramenta Go Land, e aguardar que seja finalizado a parte de configuração e indexação:
  <img src="https://user-images.githubusercontent.com/29335033/146402579-bcd1f476-cf1a-4b97-9faf-36ad9aa089ab.png"/>
  	  
	. A indexação foi finalizada com sucesso conforme mostra imagem abaixo e deva reiniciar a aplicação Go Land:
  <img src="https://user-images.githubusercontent.com/29335033/146402662-dc27ddd4-5067-46ef-b607-d5cd1572eabc.png"/>
  
	18) Para verificar a origem do repositório de cada micro serviço deve ser digitado o comando abaixo no Terminal do próprio Go Land. 
Não esqueça de acessar o diretório do serviço, conforme mostra imagem abaixo:
	
##	Git remote get-url origin
  <img src="https://user-images.githubusercontent.com/29335033/146402755-9e318c57-616a-4947-a174-7a12603d7a6b.png"/>
  	
	
	19) Após a configuração do Go Land com free5gc para fazer o Debug dos serviços, deve-se levantar os seguintes serviços :
	
	1. NRF   2. UDR   3. UDM   4. AUSF   5. NSSF   6. AMF   7. PCF   8. UPF (sudo -E ./bin/free5gc-upfd)     9. SMF   10. SERVER-WEB     11. SERVER-FRONT-END ( REACT_APP_HTTP_API_URL=http://core_ip_address:5000/api PORT=3000 yarn start )
	
	20) Deve-ser fazer o debug do serviço NRF, executando o Debug clicando com o botão direito do mouse no arquivo "nrf.go". O serviço NRF é responsável para registrar os demais microserviços, no contexto 5G.
	
	
	
	21) Se observamos a imagem abaixo, agora temos o microserviço da NRF respondendo no endereço [127.0.0.10:8000]. Este micro serviço é de rede
	
	
	Indo ao Terminal, verifica-se que o serviço NRF já criou a estrutura de dados do free5gc, veja imagem abaixo:
	
	
	. Comandos no MongoDB para verificar banco de dados e coleções e dados dos micros serviços já coletados:
	  - show databases
	  - show colletctions
	  - db.<nome_da_collection>.find().pretty()    - Exemplo:  db.NfProfile.find().pretty()
	
	
	
	22) Na pasta "config" dentro do Projeto free5gc possui um arquivo de configuração para cada função/serviço de Rede. Observa-se na imagem abaixo que no arquivo nrfcfg.yaml, o MongoDB já esta configurado com o IP e porta:
	
	
	23) Agora deve-se levantar os demais serviços: 2. UDR   3. UDM   4. AUSF   5. NSSF   6. AMF   7. PCF   8. UPF   9. SMF   10. SERVER-WEB    11. SERVER-FRONT-END 
	. O serviço de UDR faz a interface com o usuário
	
	2. UDR
	
	
	
	
	
	3. UDM
	
	
	
	
	
	
	4. AUSF   
	
	
	
	
	
	5. NSSF   
	
	
	
	
	6. AMF   
	
	
	
	
	7. PCF   
	
	
	

	
	8. UPF   
	É uma função de rede que trata de dados do usuário (plano de dados do usuário). Para subir este serviço tem que acessar via terminal no diretorio do UPF, pois foi gerado em c e necessita instalar as bibliotecas para que possa ser compilada. O requisito mínimo é a versão do kernel acima de 5.04 e para verificar no Linux utilize o comando no terminal "uname -r". Caso esteja abaixo desta versão deve ser feito uma atualização do kernel.
	
	
	
	. Para verificar os requisitos e como instalar o serviço UPF acessar o github do free5gc - free5gc/upf at b68893439706676c4372d848981fcdbe0c69a41d (github.com)
	
	
	. Caso necessite atualizar o Kernel favor executar o comando abaixo:
		 - sudo apt-get install -y linux-image-5.0.0-23-generic
	
	. Instalar bibliotecas em C para que possa ser compilado o serviço de UPF:
		sudo apt-get -y install cmake
		sudo apt-get -y install libmnl-dev
		sudo apt-get -y install autoconf
		sudo apt-get -y install libtool
		sudo apt-get -y install libyaml-dev
		
		
		sudo apt-get -y update
sudo apt-get -y install git gcc g++ cmake go libmnl-dev autoconf libtool libyaml-dev
		go get github.com/sirupsen/logrus
		
	. Caso a linha de comando "sudo apt-get -y install git gcc g++ cmake go libmnl-dev autoconf libtool libyaml-dev" dê erro, como mostra na imagem abaixo, deve-se instalar o pacote go:
	
	
	
	. Instalar o pacote go, utilize a linha de comando:
	 sudo snap install go --classic
	
	. Para instalar seguir os passos abaixo:
	
	
	
	
	
	
	
	9. SMF   
	
	
	10. SERVER-WEB    
	
	
	11. SERVER-FRONT-END 
	
	
	
![image](https://user-images.githubusercontent.com/29335033/146402971-ec1fc53c-7064-4153-b41c-c591af678934.png)

