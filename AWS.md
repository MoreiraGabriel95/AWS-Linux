# Documentação das Tarefas Realizadas

Aqui está a documentação das tarefas que foram concluídas.

## 1. Geração da Chave Pública

Para acessar o ambiente de forma segura, foi gerada uma chave pública. Essa chave será usada para autenticação.

## 2. Criação de uma Instância EC2

Uma instância EC2 foi criada com o sistema operacional Amazon Linux 2. Abaixo estão os detalhes da instância:
- **Família:** t3.small
- **Armazenamento:** 16 GB SSD

## 3. Geração e Anexação de um Elastic IP

Foi gerado um Elastic IP e anexado à instância EC2 criada anteriormente. Isso permite que a instância tenha um endereço IP estático.

## 4. Liberação de Portas de Comunicação

As seguintes portas de comunicação foram liberadas para acesso público:
- Porta 22/TCP
- Porta 111/TCP e UDP
- Porta 2049/TCP/UDP
- Porta 80/TCP
- Porta 443/TCP
