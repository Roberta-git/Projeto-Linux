# Projeto Linux: Monitoramento Automatizado de Site em AWS
 > No documento a seguir, será detalhado os passos de como criar site com monitoramento automatizado, que registra logs e envia alertas via webhook do discord.


### Índice

  1. Configuração do ambiente
  2. Instalação do servidor Web
  3. Monitoramento do script via Discord
  4. Teste e avaliação do programa
  5. Considerações finais



### Ferramentas utilizadas
- **Amazon EC2**: Servidor Ubuntu.
- **IP Elástico**: Associado à instância para acesso fixo e público.
- **Nginx**: Servidor web.
- **Webhook do Discord**: Para envio de alertas.
- **Cron**: Agendador de tarefas.





### 1. Configuração do ambiente

#### 1.1. Criação da VPC 

&nbsp;&nbsp; Para criar a VPC, acesse o painel VPC no console da AWS e clique em "Criar VPC". 

&nbsp;&nbsp; *Insira um nome para sua VPC e um IP.


 <img src="https://github.com/user-attachments/assets/903117d2-ce77-44e7-a7cb-d584e6aec882"  alt="" width="700"/>
</p>


#### 1.2 Criação das Sub-redes

&nbsp;&nbsp; Acesse "Sub-redes" no painel da VPC e clique em "Criar sub-rede" e crie duas sub-redes públicas e 2 sub-redes privadas.

&nbsp;&nbsp; *Nomeie a sub-rede, escolha uma zona de disponibilidade e um IP. 



<img src="https://github.com/user-attachments/assets/40cb4ca9-6341-4aa7-a239-90cd04d1b593"  alt="" width="700"/>
</p>



#### 1.3 Criação e associação do Gateway e configuração da tabela de rotas

&nbsp;&nbsp; Ainda no painel da VPC, vá em "Gateways de Internet", crie uma gateway com um nome simbólico e associe à VPC para permitir a conexão dos recursos com a internet.


<img src="https://github.com/user-attachments/assets/074211af-80cc-4754-bdf5-217a2904e3e7"  alt="" width="700"/>
</p>


&nbsp;&nbsp; Em "Tabela de Rotas", crie ou edite uma tabela, adicionando um destino para qualquer endereço IP e o alvo (sua gateway).


<img src="https://github.com/user-attachments/assets/1ff73393-847d-4afd-9ca3-b79a18fe93f7"  alt="" width="700"/>
</p>


#### 1.4 Criação da Instância

&nbsp;&nbsp; No painel da Ec2, clique em "Executar instância", e adicione:

&nbsp;&nbsp; *Nomes e tags

&nbsp;&nbsp; *AMI (Escolhi usar o servidor Ubuntu)

&nbsp;&nbsp; *Tipo de instância (t2.micro)

&nbsp;&nbsp; *Par de chaves (que será usado mais tarde, quando trabalharmos com o terminal).


<img src="https://github.com/user-attachments/assets/c21f4161-c437-4657-b6a8-eb344145fde3"  alt="" width="700"/>
</p>

&nbsp;&nbsp; Para a configuração de Rede:

&nbsp;&nbsp; *Selecione a VPC e a sub-rede pública

&nbsp;&nbsp; *Habilite o IP automático

&nbsp;&nbsp; *Configure o Grupo de Segurança, liberando uma porta 22(SSH) com o tipo de origem "Meu Ip" e uma porta 80(HTTP) como o tipo de origem "Qualquer lugar".


<img src="https://github.com/user-attachments/assets/4f5f08fe-cd6f-49c8-923f-260acc34e385"  alt="" width="700"/>
</p>




### 2. Instalação do servidor Web

#### 2.1. Conexão via ssh

&nbsp;&nbsp; Após a configuração do ambiente, usando o terminal, abra uma conexão no servidor da AWS via SSH através da chave privada e o IP elástico `ssh -i chave.pem ubuntu@ip`
e realize a instalação do Nginx por meio dos seguintes comandos:

  *`sudo apt update`
  
  *`sudo apt upgrade -y`
  
  *`sudo apt install nginx -y`
  
  *`sudo systemctl start nginx`
  
  *`sudo systemctl status nginx`
  

  <img src="https://github.com/user-attachments/assets/5c8a6c20-23bd-48d8-8524-635f9da4486b"  alt="" width="700"/>
</p>


#### 2.2 Criação da página HTML

&nbsp;&nbsp; Para criar a página use o comando `sudo nano /var/www/html/index.html` para abrir o arquivo index e editar o código da página.


<img src="https://github.com/user-attachments/assets/5f958469-c620-4dc4-8737-e6db5b69bbc5"  alt="" width="700"/>
</p>



*Página carregada do site:


<img src="https://github.com/user-attachments/assets/52a06ade-fb15-4a89-8c5d-38ad16a48a3c"  alt="" width="700"/>
</p>


### 3. Monitoramento do script via Discord

#### 3.1 Criação do script

&nbsp;&nbsp; Para a criação do script de monitoramento utilize o comando `sudo nano /usr/local/bin/monitorar_site.sh`.

<img src=""  alt="" width="700"/>
</p>


&nbsp;&nbsp; Para que o script possa ser executado, foi use o comando `sudo chmod +x /usr/local/bin/monitorar_site.sh`.

#### 3.2 Agendamento no Crontab

&nbsp;&nbsp; Para editar o arquivo de agendamento de tarefas utilize `sudo crontab -e` e insira o texto `* * * * * /usr/local/bin/monitorar_site.sh` que indica que o script de monitoramento rodará automaticamente a cada minuto.


### 4. Teste e avaliação do programa

&nbsp;&nbsp; Para testar o programa, verifique se o site está no ar através do comando `cat /var/log/monitoramento.log`.


<img src="https://github.com/user-attachments/assets/37e69f70-ebb0-4c43-bfbd-fcfb1041b661"  alt="" width="700"/>
</p>


&nbsp;&nbsp; Após a verificação, com o comando `sudo systemctl stop nginx`, o site sairá do ar, gerando a informação de "site fora do ar" no log e enviando um alerta para o servidor do Discord.


 *Site fora do ar:


<img src="https://github.com/user-attachments/assets/c7c6a91d-bc87-4617-bb27-43aa63065b61"  alt=""   width="700"/>
</p>



 *Registro do Log

 <img src="https://github.com/user-attachments/assets/b200c144-70b2-41a3-bfc0-2fb055f78486"  alt="" width="700"/>
</p>



 *Mensagem automática no Discord

 <img src="https://github.com/user-attachments/assets/2b864a46-60a1-4444-808d-e8376eafdf43"  alt="" width="700"/>
</p>

 

&nbsp;&nbsp; Para o site ser reativado use o comando `sudo systemctl start ngnix`.


 <img src="https://github.com/user-attachments/assets/6091d89b-6c4a-402a-8cad-2c7d21d9b54a"  alt="" width="700"/>
</p>




### 5. Considerações Finais
&nbsp;&nbsp; Com a realização do projeto foi possivel aprender sobre os comandos básicos do Linux, além de automação com Shell Script no monitoramento de servidores com conexão via Discord e integração de ferramentas modernas.





