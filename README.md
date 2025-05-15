Aqui está um exemplo funcional de `docker-compose.yml` para rodar o **Zabbix 7.2** com os principais componentes: servidor, frontend (interface web), banco de dados PostgreSQL, e o Zabbix agent. Este exemplo é baseado nas imagens oficiais do Zabbix no Docker Hub.

```yaml
version: '3.5'

services:
  postgres:
    image: postgres:15
    container_name: zabbix-postgres
    environment:
      POSTGRES_USER: zabbix
      POSTGRES_PASSWORD: zabbix_pass
      POSTGRES_DB: zabbix
    volumes:
      - ./data/postgres:/var/lib/postgresql/data
    restart: unless-stopped

  zabbix-server:
    image: zabbix/zabbix-server-pgsql:alpine-7.2-latest
    container_name: zabbix-server
    depends_on:
      - postgres
    environment:
      DB_SERVER_HOST: postgres
      POSTGRES_USER: zabbix
      POSTGRES_PASSWORD: zabbix_pass
      POSTGRES_DB: zabbix
      ZBX_HISTORYSTORAGEURL: "http://zabbix-web:8080"
    ports:
      - "10051:10051"
    volumes:
      - ./zbx_env/server:/etc/zabbix
    restart: unless-stopped

  zabbix-web:
    image: zabbix/zabbix-web-nginx-pgsql:alpine-7.2-latest
    container_name: zabbix-web
    depends_on:
      - zabbix-server
    environment:
      DB_SERVER_HOST: postgres
      POSTGRES_USER: zabbix
      POSTGRES_PASSWORD: zabbix_pass
      POSTGRES_DB: zabbix
      ZBX_SERVER_HOST: zabbix-server
      PHP_TZ: America/Sao_Paulo
    ports:
      - "8080:8080"
      - "8443:8443"
    restart: unless-stopped

  zabbix-agent:
    image: zabbix/zabbix-agent:alpine-7.2-latest
    container_name: zabbix-agent
    depends_on:
      - zabbix-server
    environment:
      ZBX_SERVER_HOST: zabbix-server
    restart: unless-stopped

volumes:
  postgres:
```

### Instruções

1. Salve esse conteúdo como `docker-compose.yml`.
2. Crie os diretórios persistentes:

   ```bash
   mkdir -p ./data/postgres ./zbx_env/server
   ```
3. Inicie os serviços:

   ```bash
   docker-compose up -d
   ```

### Acesso ao Zabbix

Após subir o ambiente, acesse:

* **Frontend**: [http://localhost:8080](http://localhost:8080)
* **Usuário padrão**: `Admin`
* **Senha padrão**: `zabbix`

Se quiser usar MySQL/MariaDB, posso adaptar para isso também. Deseja?
