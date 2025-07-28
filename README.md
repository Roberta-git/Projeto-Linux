# Documentação do Projeto-Linux
 > No projeto a seguir, será detalhado os passos de como criar uma VPC,com monitoramento automatizado.

### Índice
1.Configuração da VPC e criação do ambiente
2.Instalaçao do servidor Web
3.Monitoramento do scritp via Discord
3.Teste e avaliação do programa

### 1.Configuração da VPC e criação do ambiente

1.1.Crie a VPC pelo console

  <img src="https://github.com/user-attachments/assets/3737f3cc-a934-4770-a77f-28023de5ddd1" alt="" width="600"/>
</p>

1.2.Implemente duas sub-redes privadas e duas sub-redes públicas
  <img src="https://github.com/user-attachments/assets/a19ae5fa-617d-475d-9479-decd6e231dca"  alt="Sub-rede sendo criada" width="600"/>
</p>

   * 4 Sub-redes criadas
 <img src="https://github.com/user-attachments/assets/3925a0de-2a5d-4ba3-816e-5bac64a0169c"  alt="Sub-rede sendo criada" width="600"/>
</p>

1.3.Crie e associe o  Gateway com a VPC para o acesso à internet

 <img src="https://github.com/user-attachments/assets/426db276-5c62-4b95-b6d7-17648f67fba6"  alt="" width="600"/>
</p>


 <img src="https://github.com/user-attachments/assets/66fb25d5-6a36-45a3-8895-7a1e16e2af47"  alt="" width="600"/>
</p>

1.4.Configurae a tabela de rotas para a sub-red pública

<img src="https://github.com/user-attachments/assets/40064d48-b3d7-4423-80dd-3bc7e988a49b"  alt="" width="600"/>
</p>


 <img src="https://github.com/user-attachments/assets/3eb2476f-f1f3-4174-b95e-333830d1ae1e"  alt="" width="600"/>
</p>


### 2.Instalação do servidor Web

2.1 Criação da instância

  *Acesse Ec2 e clique em criar instânica 
  
  *Coloque as tags fornecidas:

  <img src="https://github.com/user-attachments/assets/ab193f40-7350-4e62-9e3a-81c2867d2d0b"  alt="" width="600"/>
</p>



  * Escolha uma AMI (Decidi usar Ubunto por estar mais habituada com a interface).








