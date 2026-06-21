# Monitoramento Zabbix - Docker compose 
 
O arquivo docker-compose.yml que está público em meu Github, foi configurado de forma que o
Docker cria containers. Este projeto implanta um Ambiente Completo de Monitoramento de Ativos utilizando o Zabbix 7.4 dentro de containers Docker.

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
