# Ethereum Node (Trin) + Monitoring Stack

Este projeto configura um nó da rede Ethereum Mainnet utilizando o **Trin** (cliente do Portal Network), mantendo o uso de disco abaixo de 240GB. O projeto também inclui uma stack completa de monitoramento e um explorador de blocos.

## Arquitetura
1. **Trin:** O cliente Ethereum que roda como um nó RPC na porta `8545`. Ocupa pouco espaço (limite configurado para 100GB).
2. **Prometheus:** Coleta as métricas do Trin na porta `9005`.
3. **Grafana:** Painel de monitoramento das métricas do nó (acessível na porta `3000`).
4. **Ethereum Lite Explorer:** Um painel web leve para explorar os blocos, carteiras e transações (acessível na porta `8081`).

## Como rodar no seu servidor

1. Copie a pasta `eth-node` para o seu servidor.
2. Acesse a pasta no servidor via terminal:
   ```bash
   cd /caminho/para/eth-node
   ```
3. Inicie os contêineres em segundo plano:
   ```bash
   docker compose up -d
   ```

## Como acessar as interfaces

Certifique-se de que as portas do seu servidor estão abertas/liberadas no firewall caso queira acessar remotamente, ou faça um túnel SSH.

- **Explorador de Blocos (Lite Explorer):** `http://<IP-DO-SERVIDOR>:8081`
- **Grafana (Monitoramento):** `http://<IP-DO-SERVIDOR>:3000` (Login padrão: `admin` / Senha: `admin`)
- **RPC do Ethereum:** `http://<IP-DO-SERVIDOR>:8545`

### Configurando o Lite Explorer
Quando você abrir o Lite Explorer no navegador, ele tentará se conectar ao RPC. 
No arquivo `docker-compose.yml`, a variável `APP_NODE_URL` está configurada como `http://localhost:8545`. Se você estiver acessando de outro computador (remotamente), você deve alterar essa variável no `docker-compose.yml` para o IP real do seu servidor, pois o explorador roda direto no navegador (client-side) e precisará chegar até a porta 8545 do servidor.

Exemplo de alteração no `docker-compose.yml`:
```yaml
environment:
  - APP_NODE_URL=http://<IP-REAL-DO-SERVIDOR>:8545
```
