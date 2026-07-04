# Ethereum Node (Trin) + Monitoring Stack no Coolify

Este projeto configura um nó da rede Ethereum Mainnet utilizando o **Trin** (cliente do Portal Network), mantendo o uso de disco abaixo de 240GB. O projeto também inclui uma stack de monitoramento e um explorador de blocos.

Toda a estrutura foi otimizada para ser implantada facilmente através do **Coolify v4**.

## Como realizar o Deploy no Coolify

A melhor forma de subir essa stack no Coolify é utilizando o método de repositório Git, pois ele copiará os arquivos de configuração do Prometheus e do Grafana automaticamente.

### Passo 1: Suba este projeto para um repositório Git
Crie um repositório no GitHub ou GitLab e faça o push de todos os arquivos desta pasta (`docker-compose.yml`, pasta `grafana/`, `prometheus.yml`, etc).

### Passo 2: Adicione o Recurso no Coolify
1. Abra o painel do seu Coolify.
2. Clique em **Add New Resource** e escolha a opção **Git Repository**.
3. Selecione o repositório que você acabou de criar.
4. Quando o Coolify perguntar o tipo de Build Pack, selecione **Docker Compose**.
5. Em "Docker Compose Location", certifique-se de que está apontando para o arquivo `/docker-compose.yml`.

### Passo 3: Configurar os Domínios (Opcional, mas Recomendado)
Se você for apontar domínios (ex: `rpc.seusite.com`, `explorer.seusite.com`) para as suas ferramentas usando o proxy reverso do Coolify, siga estas instruções **antes de clicar em Deploy**:

No painel do Coolify, ele listará os seus containers (`trin`, `grafana`, `explorer`).
- Para o **Trin**, adicione o seu domínio e direcione para a porta **8545**.
- Para o **Grafana**, adicione o domínio e direcione para a porta **3000**.
- Para o **Explorer**, adicione o domínio e direcione para a porta **80**.

### Passo 4: Configurar a URL do Explorer
O Lite Explorer roda diretamente no navegador do usuário e precisa saber onde o seu RPC (Trin) está hospedado para buscar os blocos.
No Coolify, vá em **Environment Variables** do seu recurso e adicione/altere a variável `APP_NODE_URL`:
- Se você **não** configurou domínios: coloque `http://<IP-DO-SEU-SERVIDOR>:8545`
- Se você **configurou** um domínio para o Trin: coloque `https://rpc.seusite.com` (o domínio escolhido).

### Passo 5: Fazer o Deploy
Clique em **Deploy** no Coolify! Ele fará o build, criará os volumes persistentes (`trin_data`, `prometheus_data`, `grafana_data`) e iniciará toda a sua stack.

---

**Login do Grafana:**
O Grafana iniciará no domínio/porta configurado. 
Usuário padrão: `admin` / Senha: `admin`
