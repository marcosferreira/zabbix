
# Zabbix via Docker Compose

Repositório para facilitar a implantação do **Zabbix 7 LTS** utilizando **Docker Compose** com suporte a **PostgreSQL** como banco de dados e frontend via **NGINX + PHP**.

> ✅ Projeto mantido por [Marcos Ferreira](https://github.com/marcosferreira)

---

## 📦 Componentes

Este ambiente Docker Compose inclui:

- PostgreSQL (banco de dados)
- Zabbix Server
- Zabbix Web (NGINX + PHP)
- Suporte para `.env` com variáveis customizáveis

---

## 🚀 Como usar

### 1. Clone o repositório

```bash
git clone https://github.com/marcosferreira/zabbix.git
cd zabbix
````

### 2. Configure o arquivo `.env`

Edite o arquivo `.env` com os parâmetros necessários. Exemplo:

```env
# Versão do Zabbix
ZABBIX_VERSION=7.0.1
ZABBIX_LOCAL_IMAGE_TAG_POSTFIX=

# Banco de dados
DB_SERVER_HOST=postgres
POSTGRES_USER=zabbix
POSTGRES_PASSWORD=zabbix
POSTGRES_DB=zabbix

# Web
ZBX_SERVER_HOST=zabbix-server
PHP_TZ=America/Sao_Paulo
```

### 3. Suba os containers

```bash
docker compose up -d
```
