# Documentação do Projeto-Linux
 > No documento a seguir, será detalhado os passos de como criar site com monitoramento automatizado.

### Índice
1.Configuraçãodo ambiente
2.Instalaçao do servidor Web
3.Monitoramento do scritp via Discord
3.Teste e avaliação do programa

### 1. Configuração do ambiente

Na configuração do ambiente, foram criados a VPC, sub-redes (duas públicas e duas privadas), internt Gateway, tabelas de rotas e a instânica (liberando portas 22 (SSH) e 80 (http)).

 <img src="https://github.com/user-attachments/assets/87ce19e1-a15b-4309-b81a-5931c8450a05" alt="" width="700"/>
</p>


### 2. Instalação do servidor Web

2.1 Conexão via ssh
Após a configuração do amiente, usando o terminal, foi aberto uma conexão no servidor da AWS via SSH, utilizando minha chave privada e o Ip elástico e realizado a instalação do Nginx por meio dos seguintes comandos:
  *sudo apt update
  *sudo apt upgrade -y
  *sudo apt install nginx -y
  *sudo systemctl start nginx
  *sudo systemctl status nginx

  <img src=""" width="700"/>
</p>










