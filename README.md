## Apresentação

	. Este trabalho contém o script sobre como criar uma rede free5gc subindo o serviço de NWDAF para que posso coletar dados de dispositivos móveis e gerar insights através de dashboards para análise de anomalias de comportamento do dispositivo.
	. A NWDAF foi definido no 3GPP TS 29.520 que incorpora interfaces padrão da arquitetura baseada em serviço para coletar dados por assinatura ou modelo de solicitação de outras funções de rede e procedimentos semelhantes. O objetivo é fornecer funções analíticas na rede para automação ou geração de relatórios, resolvendo os principais desafios de interface ou formato personalizado.
	. Num ambiente onde está se “ouvindo” uma rede 5G (Free5GC) coletando dados para serem imputados e gerados insights por meios de dashboards para que possam analisados e orientem na solução de possíveis anomalias geradas e identificadas em eventos de sinalização e comportamento de dispositivos. Assim, coletando diferente tipos de dados será possível ver a causa da anomalia e obtendo uma assertividade significativa na solução do problema.
	
Antes de iniciar a instalação e configuração, conforme documentação da free5gc é recomendado o seguinte ambiente:
• Software
	○ OS: Ubuntu 18.04
	○ gcc 7.3.0
	○ Go 1.14.4 linux/amd64
	○ kernel version 5.0.0-23-generic

• Minimum Hardware
	○ CPU: Intel i5 processor
	○ RAM: 4GB
	○ Hard drive: 160GB
	○ NIC: Any 1Gbps Ethernet card supported in the Linux kernel
• Recommended Hardware
	○ CPU: Intel i7 processor
	○ RAM: 8GB
	○ Hard drive: 160GB
	○ NIC: Any 10Gbps Ethernet card supported in the Linux kernel

## Script: Instalação e Configuração

	1) Instalar as ferramentas: Visual Studio Code, NodeJS, GoLand, GO, Curl, NPM, Net-tools, MongoDB, Java, OpenSSH, Python, Yarn. Executar primeiro  "sudo apt-get update" para atualização de pacotes

	. Para verificar a versão de instalação do Nodejs, digitar: nodejs --version
	. Para verificar a versão de instalação do Visual Studio Code, digitar: code --version

	. Visual Studio Code: 
	 sudo apt install software-properties-common apt-transport-https wget
	 wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
	 sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
	 sudo apt install code
	  
	. Nodejs: 
	 sudo snap install nodejs
	
	  - As vezes é necessário instala o npm, que é o pacote gerenciador do Nodejs
	   sudo apt install npm
	
			§ Caso tenha algum problema com a versão do NodeJs os comandos abaixo utilizando a versão estável para o free5gc
		sudo apt-get remove nodejs
		sudo apt install wget
		wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
		source ~/.profile
		nvm install 14.17.5
		
			§ Verifique se a instalação ocorreu com sucesso checando a versão do Node.js:
		node --version
	
	. Goland: 
	  sudo apt-get install snapd
	  sudo snap install goland --classic
	
	. Go:
	  sudo snap install go --channel=1.14/stable --classic
	  go version
	
	. NetTools:
	  sudo apt-get install net-tools
	
	. Curl:
	  sudo apt install curl
	
	. NPM:
	  sudo apt install npm
	
	. MongoDB: 
	  1. Instalar o MongoDB
	  sudo apt -y update
  	  sudo apt -y install mongodb wget git
	
	  2. Execute o comando systemctl a seguir para iniciar o serviço MongoDB:
	  sudo systemctl start mongodb
	 
	  3. Verificar o status do serviço:
	  sudo systemctl status mongodb
	 
	  4. Depois de confirmar que ele está funcionando como esperado, habilite o serviço MongoDB para iniciar durante a inicialização:
	  sudo systemctl enable mongodb
	
	  5. Para verificar o MongoDB inicializar com o comando "Mongo" e para ver os databases instalado, executar as linhas de comando em sequencia: 
	  mongo
  	  show databases
	
	. OpenSSH: 
	  1. Instalando o openssh:
	   sudo apt-get update
	
	   sudo apt-get install openssh-server
	
	  2. Ativando o serviço
	   sudo service ssh status
	
	  3. Verificando se o serviço está ativo e funcionando
	   sudo systemctl status sshd
	
	  4. Habilitando conexões SSH em seu host:
	   sudo ufw allow ssh
	
	   - Se não tiver certeza se está usando ativamente o firewall UFW, execute o comando
	     sudo ufw status
	
	  5. Verificando se o serviço está habilitado ou não:
	   sudo systemctl list-unit-files | grep enabled | grep ssh
	
	     - Se não houver resultados em seu terminal, você deve “habilitar” o serviço para que seja iniciado no momento da inicialização
	       sudo systemctl enable ssh
	
	  6. Reiniciando seu servidor SSH para aplicar as alterações:
	   sudo systemctl restart sshd
	
	  7. Verificar se o serviço foi reiniciado:
	   sudo systemctl status sshd
	
	. Java: 
	  1. Instalando o java:
	   sudo apt-get update
	   sudo apt install default-java  
	
	. Yarn:   
	   sudo apt-get update
	    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
	  echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
	  sudo apt update && sudo apt install yarn
	
	. Python  
	sudo apt update && apt -y install python-minimal && sudo apt -y install git && sudo apt -y install ansible

	
	2) Criar um diretório
	. mkdir openapi_teste
	 cd openapi_teste
	
	3) Instalar o Editor Texto -Editor de linha de comando (CLI)
  	. npm install @openapitools/openapi-generator-cli -g
          openapi-generator-cli version-manager set 5.3.0
	
	4) Criar o arquivo  TS29520_Nnwdaf_Analytics.yaml
	  touch TS29520_Nnwdaf_AnalyticsInfo.yaml
	. Verificar se o arquivo foi criado corretamente
	
	5) Repositório que tenha a função e serviço do NWDAF
	site:github.com Nnwdaf_AnalyticsInfo.yaml
	
  <img src="https://user-images.githubusercontent.com/29335033/146395128-dca01f3b-e59f-4219-96cc-00b118ada528.png"/>
  
  <img src="https://user-images.githubusercontent.com/29335033/146399991-9d99c705-ee4e-4aac-bb3f-310e38817239.png"/>
	
	
	. Depois de clicar em RAW, copiar tudo para colar no arquivo "TS29520_Nnwdaf_AnalyticsInfo.yaml":
	
	--> Caso nencessite, dar permissão de leitura e escrita neste diretório (openapi_teste)
	  chown <usaurio> -R
		
	6) Abrir o Vidual Studio Code e cola o código copiado do arquivo do GitHub  "TS29520_Nnwdaf_AnalyticsInfo.yaml":
  
  <img src="https://user-images.githubusercontent.com/29335033/146400504-71977d60-1a0f-44fb-9a9e-73794e42377b.png"/>
	
	. Este arquivo .YAML foi implementado de acordo com as prerrogativas doa openapi seguindo a especificação da 3gpp que descreve o micro serviço analytics Info para ser provido pela NWDAF.
	. Também outro serviço que é gerado sobre a sobrescrita de eventos
	
	7) Criar um diretório chamado "Deploy"
  <img src="https://user-images.githubusercontent.com/29335033/146400800-985f0a3f-4cd1-4233-9b67-c12389c9c63d.png"/>
  	
	8) Em seguida abrir o Terminal pelo próprio Visual Code
  <img src="https://user-images.githubusercontent.com/29335033/146400978-9436b594-ca77-4d96-97fd-0cc45b57989e.png"/>  	
	
	9) Em seguida aplicar as prerrogativas da máquina com o comando
	 . sudo su
  <img src="https://user-images.githubusercontent.com/29335033/146401113-08c53d5c-8d0f-43b8-a621-a6dd88d01953.png"/>	
           . Acessar o "deploy" em seguida
	
	10) Mover o arquivo "TS29520_Nnwdaf_AnalyticsInfo.yaml" para dentro deste diretório
  <img src="https://user-images.githubusercontent.com/29335033/146401222-9fee119a-b572-407d-9e0d-6a538698b4a6.png"/>
  
	11) Em seguida, executar o comando para fazer a leitura do código .YAML com o CLI que foi instalado anteriormente gera e faça a construção dos "scafolds" em código fonte.
  <img src="https://user-images.githubusercontent.com/29335033/146401300-a06d0173-0a59-4974-b688-22eff5ae3b8e.png"/>
   	
	. sudo openapi-generator-cli generate -i TS29520_Nnwdaf_AnalyticsInfo.yaml -g go --skip-validate-spec -o api/Nnwdaf_AnalyticsInfo/
	
	OBSERVAÇÃO: Caso encontra a mensagem de erro: "openapi-generator-cli command not found" , execute o comando no Terminal dentro do diretório "/openapi_teste/deploy":
	. openapi-generator-cli generate -i TS29520_Nnwdaf_AnalyticsInfo.yaml -g go --skip-validate-spec -o api/Nnwdaf_AnalyticsInfo/
  	
	12) O mecanismo do openapi fez todo mecanismo do arquivo .yaml e dentro do diretório "Deploy" esta criado com sucesso:
  <img src="https://user-images.githubusercontent.com/29335033/146401463-a7e1b90e-f500-47d9-a5c6-ef411e2a54f8.png"/>
  	
	13) Dentro da pasta Deploy possui a pasta api
	. Nesta pasta tem diversos arquivos .go
	. Tudo isto com as devidas dependências, com a estrutura de conexão com as apis,  com os endpoints determinados lá na especificações, todos esses arquivos .go e as subpastas dentro de api foram gerados e construído através daquele arquivo .yaml. Aqui já possui too o scafuld inicial necessário para começar a trabalhar e construir a implementação de AnalyticsInfo. Estão tudo estruturado para começar a implementar a api
	- O ideal seria pegar a espeficição e fazer um de_para dessas especificações.
	
	. Assim foi gerado o código GO a partir dos .YML que especificam a NWDAF, fazendo uso de um CLI para gerar código a partir de especificações do arquivo .YML
	
	14) Agora implementar o núcleo free5gc, implementar esta ambiente de desenvolvimento em modo depuração com uma versão da NWDAF (que esta em construção) que coleta ANF.
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
	. Git remote get-url origin
  <img src="https://user-images.githubusercontent.com/29335033/146402755-9e318c57-616a-4947-a174-7a12603d7a6b.png"/>
  		
	19) Após a configuração do Go Land com free5gc para fazer o Debug dos serviços, deve-se levantar os seguintes serviços :
	
	1. NRF   2. UDR   3. UDM   4. AUSF   5. NSSF   6. AMF   7. PCF   8. UPF (sudo -E ./bin/free5gc-upfd)     9. SMF   10. SERVER-WEB     11. SERVER-FRONT-END ( REACT_APP_HTTP_API_URL=http://core_ip_address:5000/api PORT=3000 yarn start )
	
	20) Deve-ser fazer o debug do serviço NRF, executando o Debug clicando com o botão direito do mouse no arquivo "nrf.go". O serviço NRF é responsável para registrar os demais microserviços, no contexto 5G.
  <img src="https://user-images.githubusercontent.com/29335033/146403520-f761e320-9e50-43b4-afd3-b317e8125428.png"/> 	
	
	21) Se observamos a imagem abaixo, agora temos o microserviço da NRF respondendo no endereço [127.0.0.10:8000]. Este micro serviço é de rede
  <img src="https://user-images.githubusercontent.com/29335033/146403908-ac3c2f8a-cd91-4574-8a60-2aefca8c94f4.png"/> 		
	
	22) Na pasta "config" dentro do Projeto free5gc possui um arquivo de configuração para cada função/serviço de Rede. Observa-se na imagem abaixo que no arquivo nrfcfg.yaml, o MongoDB já esta configurado com o IP e porta:
  <img src="https://user-images.githubusercontent.com/29335033/146402755-9e318c57-616a-4947-a174-7a12603d7a6b.png"/> 		
	
	23) Agora deve-se levantar os demais serviços: 2. UDR   3. UDM   4. AUSF   5. NSSF   6. AMF   7. PCF   8. UPF   9. SMF   10. SERVER-WEB    11. SERVER-FRONT-END 
	. O serviço de UDR faz a interface com o usuário
	
	2. UDR
  <img src="https://user-images.githubusercontent.com/29335033/146404238-6e66e064-33e5-4722-9ed3-34e4c0afa509.png"/> 		
  <img src="https://user-images.githubusercontent.com/29335033/146404338-ebb726e5-d5da-4245-868d-02e2d44639a3.png"/> 	
  
	Indo ao Terminal, verifica-se que o serviço NRF já criou a estrutura de dados do free5gc, veja imagem abaixo:
  <img src="https://user-images.githubusercontent.com/29335033/146404135-3ee14295-9926-4316-b355-d3802eeb7e39.png"/> 	
	
	. Comandos no MongoDB para verificar banco de dados e coleções e dados dos micros serviços já coletados:
	  - show databases
	  - show colletctions
	  - db.<nome_da_collection>.find().pretty()    - Exemplo:  db.NfProfile.find().pretty()  
	
	3. UDM
  <img src="https://user-images.githubusercontent.com/29335033/146404512-76cb73a7-4e54-499b-b7a6-9741a3ea9d85.png"/> 	
  <img src="https://user-images.githubusercontent.com/29335033/146404583-c787acf7-0126-4a02-a07b-96bffef57c13.png"/> 		
	
	4. AUSF   
  <img src="https://user-images.githubusercontent.com/29335033/146404666-8d9d4609-698a-4c21-a047-a700e7a71252.png"/> 	
  <img src="https://user-images.githubusercontent.com/29335033/146404758-c068c4dc-d29f-4f51-906e-36bf6d3a323a.png"/> 		
	
	5. NSSF   
  <img src="https://user-images.githubusercontent.com/29335033/146404815-7e3ccfed-6997-467e-bb62-576af50a5f33.png"/> 	
  <img src="https://user-images.githubusercontent.com/29335033/146404922-01514953-0a39-4ded-94b6-86263a036bdd.png"/> 		
	
	6. AMF   
  <img src="https://user-images.githubusercontent.com/29335033/146405027-475a8c8e-6ccf-4117-923a-e8c9d50c18ac.png"/> 	
  <img src="https://user-images.githubusercontent.com/29335033/146405137-bc95731b-0c21-4dd9-a944-6336e422d7d1.png"/> 		

	7. PCF   
  <img src="https://user-images.githubusercontent.com/29335033/146405217-ec205605-6ede-47ce-b4f0-d86098bc46e7.png"/> 	
  <img src="https://user-images.githubusercontent.com/29335033/146405306-7883decf-4772-4905-b25e-6939de629f7c.png"/> 		
	
	8. UPF   
	É uma função de rede que trata de dados do usuário (plano de dados do usuário). Para subir este serviço tem que acessar via terminal no diretorio do UPF, pois foi gerado em c e necessita instalar as bibliotecas para que possa ser compilada. O requisito mínimo é a versão do kernel acima de 5.04 e para verificar no Linux utilize o comando no terminal <b>"uname -r"</b>. Caso esteja abaixo desta versão deve ser feito uma atualização do kernel.
  <img src="https://user-images.githubusercontent.com/29335033/146405446-7d893759-8c34-4b5f-a53e-ab410bba3ec0.png"/> 		
	
	. Para verificar os requisitos e como instalar o serviço UPF acessar o github do free5gc - free5gc/upf at b68893439706676c4372d848981fcdbe0c69a41d (github.com)
  <img src="https://user-images.githubusercontent.com/29335033/146405994-d7fc63d2-851c-47e0-9807-c91495ac3ecd.png"/> 		
	
	a. Caso necessite atualizar o Kernel favor executar o comando abaixo:
		 - sudo apt-get install -y linux-image-5.0.0-23-generic
	
	b. Para verificar os requisitos e como instalar o serviço UPF acessar o github do free5gc (free5gc/upf (github.com))
	  . https://github.com/free5gc/upf
	  
	c. Executar as linhas de comando abaixo
		sudo apt-get -y update
sudo apt-get -y install git gcc g++ cmake go libmnl-dev autoconf libtool libyaml-dev
		go get github.com/sirupsen/logrus
		
	d. No caso de erro da linha de comando "sudo apt-get -y install git gcc g++ cmake go libmnl-dev autoconf libtool libyaml-dev", deve instalar bibliotecas abaixo de forma separada para que possa ser compilado o serviço de UPF:
		sudo apt-get -y install cmake
		sudo apt-get -y install libmnl-dev
		sudo apt-get -y install autoconf
		sudo apt-get -y install libtool
		sudo apt-get -y install libyaml-dev
	
	 e. Criar um túnel de conexão do gtp, executar os comandos abaixo no diretório "free5gc": 
		git clone -b https://github.com/free5gc/gtp5g.git
		    . Caso dê erro o comando acima, favor executar a linha abaixo:
		      git clone https://github.com/free5gc/gtp5g.git
		
		cd gtp5g
		git checkout -b v0.3.2
		make
		sudo make install
	   
	 f. Fazer o Build, compilar o plano de usuário da UPF. Deve acessar o diretório "/free5gc/NFs/upf/":
		mkdir build
		cd build
		cmake ..
		make -j `nproc`
		
		. Caso apresente o erro: "./configure: line 2950: syntax error near unexpected token LIBMNL", executar as linhas abaixo no diretorio "/Home"
		1) sudo apt install -y build-essential automake pkg-config
		2) git clone  https://github.com/linux-test-project/ltp.git
		3) cd ltp
		4) make autotools
		5) ./configure
		
		Em seguida, executar novamente a linha de comando: make -j `nproc`
	
	 g. Configuração de rede, executando as linhas de comando abaixo:
	     sudo sysctl -w net.ipv4.ip_forward=1

	     sudo iptables -t nat -A POSTROUTING -o {{ internet_network_interface }} -j MASQUERADE
	     . Para saber o nome da interface de rede {{ internet_network_interface }} , executar a linha de comando:
	        ifconfig
	              
	  . Redirecionamento da interface de rede:
	   # sudo iptables -t nat -A POSTROUTING -o enps0s3 -j MASQUERADE (coloque o nome da sua interface de rede)
	   sudo iptables -A FORWARD -p tcp -m tcp --tcp-flags SYN,RST SYN -j TCPMSS --set-mss 1400
	
	  . Recomendado parar o firewall com a linha de comando:
	   sudo systemctl stop ufw
	
	 h. Colocar para executar a UPF, deve estar no diretório "/free5gc/NFs/upf/build" com a linha de comando:
	   sudo -E ./bin/free5gc-upfd
		
	9. SMF   
  <img src="https://user-images.githubusercontent.com/29335033/146615751-542dcc63-1ed4-4a01-b3cc-686ad7e152f4.png"/> 			
  <img src="https://user-images.githubusercontent.com/29335033/146615824-387a0437-44ed-44fa-8796-d9608c609790.png"/> 
  
	10. SERVER-WEB    
	. Acessar o diretório "free5gc"   
	cd webconsole
	cd frontend
	yarn install
	yarn build
	rm -rf ../public
	cp -R build ../public
	cd..
	go build -o bin/webconsole server.go
	
	. Será criado uma interface gráfica para fazer a gestão dos dispositivos.
	
  <img src="https://user-images.githubusercontent.com/29335033/146615919-a428cd73-5283-40c9-99a9-94ef2598e508.png"/> 				
	. Agora deve iniciar o serviço:
	REACT_APP_HTTP_API_URL=htpp://127.0.0.1:5000/api PORT=3000 yarn start

	
	11. SERVER-FRONT-END 		


