# Projeto Linux: Monitoramento Automatizado de Site em AWS
 > No documento a seguir, será detalhado os passos de como criar site com monitoramento automatizado, que registra logs e envia alertas via webhook do discord.


### Índice

  1. Configuração do de ambiente
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

1.1. Criação da VPC e sub-redes

&nbsp;&nbsp; Para criar a VPC, acesse o painel VPC no console da AWS e clique em criar VPC. 
&nbsp;&nbsp; *Insira um nome para sua VPC e um Ip (terminar)


 <img src="https://github.com/user-attachments/assets/5c8a6c20-23bd-48d8-8524-635f9da4486b"  alt="" width="700"/>
</p>




### 2. Instalação do servidor Web

2.1. Conexão via ssh

&nbsp;&nbsp; Após a configuração do ambiente, usando o terminal, foi aberto uma conexão no servidor da AWS via SSH através da minha chave privada e o Ip elástico e realizado a instalação do Nginx por meio dos seguintes comandos:

  *`sudo apt update`
  
  *`sudo apt upgrade -y`
  
  *`sudo apt install nginx -y`
  
  *`sudo systemctl start nginx`
  
  *`sudo systemctl status nginx`
  

  <img src="https://github.com/user-attachments/assets/5c8a6c20-23bd-48d8-8524-635f9da4486b"  alt="" width="700"/>
</p>


2.2 Criação da página HTML

&nbsp;&nbsp; Para criar a página foi usado o comando `sudo nano /var/www/html/index.html` para abrir o arquivo index e editar o código da página.


<img src="https://github.com/user-attachments/assets/5b1c8afa-5b5b-44f8-a745-0d061856018d"  alt="" width="700"/>
</p>



*Página carregada do site:


<img src="https://github.com/user-attachments/assets/f957967e-13c4-498c-a3c0-a47b8fe7ad45"  alt="" width="700"/>
</p>


### 3. Monitoramento do script via Discord

3.1 Criação do script

&nbsp;&nbsp; Para a criação do script de monitoramento foi executado o comando `sudo nano /usr/local/bin/monitorar_site.sh`.

<img src="https://github.com/user-attachments/assets/890e2aba-ca30-4a22-9889-655df4442040"  alt="" width="700"/>
</p>


&nbsp;&nbsp; Para que o script possa ser executado, foi usado o comando `sudo chmod +x /usr/local/bin/monitorar_site.sh`.

3.2 Agendamento no crontab

&nbsp;&nbsp; Para editar o arquivo de agendamento de tarefas foi utilizado o comando `sudo crontab -e` e inserido o texto `* * * * * /usr/local/bin/monitorar_site.sh` que indica que o script de monitoramento rodará automaticamente a cada minuto.


### 4. Teste e avaliação do programa

&nbsp;&nbsp; Para testar o programa, foi verificado se o site estava no ar através do comando `cat var/log/monitoramento.log`.


<img src="https://github.com/user-attachments/assets/37e69f70-ebb0-4c43-bfbd-fcfb1041b661"  alt="" width="700"/>
</p>


&nbsp;&nbsp; Após a verificação, com o comando `sudo systemctl stop nginx`, o site saiu do ar, gerando a informação de "site fora do ar" no log e enviado um alerta para o servidor do Discord.


 *Site fora do ar:


<img src="https://github.com/user-attachments/assets/c7c6a91d-bc87-4617-bb27-43aa63065b61"  alt=""   width="700"/>
</p>



 *Registro do Log

 <img src="https://github.com/user-attachments/assets/b200c144-70b2-41a3-bfc0-2fb055f78486"  alt="" width="700"/>
</p>



 *Mensagem automática no Discord

 <img src="https://github.com/user-attachments/assets/2b864a46-60a1-4444-808d-e8376eafdf43"  alt="" width="700"/>
</p>

 

&nbsp;&nbsp; Para o site ser reativado foi usado o comando `sudo systemctl start ngnix`.


 <img src="https://github.com/user-attachments/assets/6091d89b-6c4a-402a-8cad-2c7d21d9b54a"  alt="" width="700"/>
</p>




### 5. Considerações Finais
&nbsp;&nbsp; Com a realização do projeto foi possivel aprender sobre os comandos básicos do Linux, além de automação com Shell Script no monitoramento de servidores com conexão via Discord e integração de ferramentas modernas.





