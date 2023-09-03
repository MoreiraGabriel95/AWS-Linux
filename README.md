# Parte prática

## 1.1 Gerar uma chave pública para acesso ao ambiente

Existem basicamente três maneiras de gerarmos chaves públicas para acessar o ambiente:

- Durante a criação da instância, você pode gerar uma chave de acesso.
- Após a criação da instância, é possível importar uma chave. Isso pode ser feito tanto usando a aplicação Putty disponível para sistemas operacionais Windows quanto o terminal do Linux.  <br/>

## 1.2 Criar uma instância EC2 com o sistema operacional Amazon Linux 2 (t3.small, 16GB SSD)

Para criar uma instância EC2 com as especificações desejadas, siga as etapas abaixo:

1. Acesse o AWS Console.
2. Clique em "EC2".
3. Crie uma nova instância EC2 com as configurações desejadas.
4. Conclua o assistente de criação da instância.  <br/>

## 1.3 Gerar um Elastic IP e anexar à instância EC2

Para garantir um endereço IP estático para a sua instância EC2, siga estas etapas:

1. No AWS Console, clique em "Elastic IPs".
2. Crie um novo Elastic IP.
3. Após a criação, associe-o à instância EC2.  <br/>

## 1.4 Liberar as portas de comunicação para acesso público

Para permitir o acesso público à instância, siga estas etapas:

1. No campo de detalhes da instância, vá para "Grupos de Segurança".
2. Selecione o grupo de segurança associado à instância.
3. Clique na guia "Regras de Entrada".
4. Adicione as regras, uma a uma, para liberar as portas desejadas.  <br/>

## 2.1 Configurar o NFS entregue

Para instalar o NFS no Amazon Linux 2, é necessário executar os seguintes comando:

sudo yum install nfs-utils  <br/>
<br/>

## 2.2 Criar um diretório dentro do filesystem do NFS com seu nome:

sudo mkdir /mnt/nfs_share/gabriel  <br/>
  <br/>

## 2.3 Subir um Apache no servidor:

Instalar o Apache:

sudo yum install httpd  <br/>
  <br/>

Iniciar e habilitar o Apache:

sudo systemctl start httpd
sudo systemctl enable httpd  <br/>
  <br/>

## 2.4 Criar um script de validação do serviço:

#!/bin/bash
timestamp=$(date "+%Y-%m-%d %H:%M:%S")
service_name="Apache"
status=$(sudo systemctl is-active httpd)

if [ "$status" = "active" ]; then
  message="ONLINE"
  output_file="/mnt/nfs_share/gabriel/online.txt"
else
  message="OFFLINE"
  output_file="/mnt/nfs_share/gabriel/offline.txt"
fi

echo "$timestamp $service_name $status $message" > "$output_file"  <br/>
  <br/>

Torne o script executável:

chmod +x check_apache_status.sh  



## 2.5 Preparar a execução automatizada do script a cada 5 minutos:

Adicionar uma entrada ao crontab para executar o script a cada 5 minutos:

crontab -e  <br/>
  <br/>

Adicionar a seguinte linha ao arquivo (ajuste o caminho para o seu script):

*/5 * * * * /caminho/para/check_apache_status.sh
