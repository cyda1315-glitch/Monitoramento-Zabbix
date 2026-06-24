## PROGRAMAÇÃO PARA REDES 
### Alunos: Aparecida Cristina Silva e Lucas de figueiredo Gomes
  # TEMA
# Monitoramento Zabbix - Docker compose 
 
O arquivo docker-compose.yml que está público em meu Github, este projeto implanta um Ambiente Completo de Monitoramento de Ativos utilizando o Zabbix dentro de containers Docker.

## Conteúdo do Projeto (Componentes):
### mysql-server (Banco de Dados): 
Armazena todos os dados de configuração, histórico de monitoramento, usuários e alertas do Zabbix.

### zabbix-server(O Cérebro): 
Processa os dados recebidos, executa as checagens, calcula triggers (gatilhos de problemas) e envia notificações.

### zabbix-web (A Interface): 
Interface gráfica (Nginx + PHP) rodando na porta 8080 para você visualizar os gráficos, cadastrar hosts e gerenciar o sistema. O fuso horário está configurado corretamente para Cuiabá.

### zabbix-agent2 / App1 / App2 / zabbix-server-agent (Os Agentes): 
São quatro instâncias do agente do Zabbix. Eles simulam os servidores/aplicações que serão monitorados. O zabbix-agent2 principal se destaca por ter acesso ao /var/run/docker.sock, permitindo monitorar o status do próprio Docker.

### rede-cida (Rede Isolada): 
Uma rede interna customizada (172.30.0.0/24) para que os containers se comuniquem de forma segura e com IPs fixos.

# O Ubuntu precisa ter
Antes de rodar o projeto, o seu servidor ou máquina virtual com Ubuntu precisa ter as seguintes ferramentas instaladas:

### 1. Docker: O motor que roda os containers.

### 2. Docker Compose V2: O utilitário que lê o seu arquivo docker-compose.yml e monta a estrutura.

### 3. Git (Opcional, mas recomendado): Para clonar ou versionar sua pasta de trabalho.

# Comandos para preparar o Ubuntu:
### Atualizar a lista de pacotes

sudo apt update && sudo apt upgrade -y

### Instalar o Docker e o Docker Compose

sudo apt install docker.io docker-compose-v2 git -y

### Adicionar seu usuário ao grupo do docker (para não precisar usar 'sudo' toda hora)

sudo usermod -aG docker $USER

## ATENÇÃO: Após o comando acima, deslogue e logue novamente no Ubuntu para aplicar a mudança.


# Criar a pasta do projeto
No terminal, crie uma pasta dedicada para organizar os arquivos e entre nela:

mkdir -p ~/zabbix-cida

cd ~/zabbix-cida

# Criar o arquivo de configuração
## Crie o arquivo docker-compose.yml utilizando o editor de texto do terminal (como o nano):

nano docker-compose.yml

# Subir os containers

docker compose up -d

# Verifique os containers:

docker ps

# Primeiro Acesso a interface na Web

http://localhost:8080 ou https://localhost:9443

## Dados de Login Padrão do Zabbix:

Usuário padrão: Admin 

Senha padrão: zabbix

# Cadastrar os Agentes

## Host name: Host (Deve ser idêntico ao ZBX_HOSTNAME do container)

Modelos: Linux by Zabbix agent ou Docker by Zabbix agent 2

Host groups: Linux servers 

Interfaces (Agent):  → Endereço IP: 172.30.0.40  → Porta: 10050

## Cadastrando o Agente App1

Nome do host: App1

Modelos: Linux by Zabbix agent 

Host groups: Linux servers

Interfaces (Agent):  → Endereço IP: 172.30.0.50  → Porta: 10050

## Cadastrando o Agente App2

Nome do host: App2

Modelos: Linux by Zabbix agent

Host groups: Linux servers

Interfaces (Agent):  → Endereço IP: 172.30.0.60   → Porta: 10050

## Cadastrando o Agente do Próprio Servidor Zabbix

Este agente monitora a própria saúde e métricas do container onde o Zabbix está processando os dados.

Nome do host: ZabbixServer

Modelos: Linux by Zabbix agent

Host groups: Linux servers

Interfaces (Agent):  → Endereço IP: 172.30.0.70   →  Porta: 10050


# Informações Gerais da Rede (rede-cida)
## Sub-rede (Subnet): 172.30.0.0/24

## Máscara de Rede: 255.255.255.0

## Gateway (Roteador da Rede): 172.30.0.1


<img width="2528" height="1684" alt="Mapa de instrutura" src="https://github.com/user-attachments/assets/4edc5aac-572e-4939-b97d-2d0b42711af5" />


# Clonar o Repositório do GitHub

git clone https://github.com/cyda1315-glitch/Monitoramento-Zabbix.git

## Entre na pasta:
cd zabbix-cida

## Verificar os Arquivos do Projeto

Confira se o arquivo docker-compose.yml está presente:

ls

### Deve aparecer:

docker-compose.yml

## levantar os Containers

Execute:

docker compose up -d

O Docker fará automaticamente:

→ Download das imagens.

→ Criação da rede rede-cida.

→ Criação dos volumes.

→ Inicialização dos containers.

## Verificar os Containers

docker ps

Os seguintes containers devem aparecer:

→ zabbix-mysql

→ zabbix-server

→ zabbix-web

→ zabbix-agent2

→ App1

→ App2

→ zabbix-server-agent


---
### 🤝 Agradecimentos

---

### 💙 Obrigado por acompanhar até aqui!

Este projeto foi desenvolvido com o objetivo de consolidar e compartilhar conhecimento prático em redes Docker e monitoramento com Zabbix. 
Qualquer feedback ou sugestão de melhoria via *Pull Request* ou *Issues* será muitíssimo bem-vindo!

Se esse material foi útil para os seus estudos, apoie deixando uma ⭐️ no repositório!

---

