# Zabbix 7.2 com Docker Compose

Repositório para facilitar a implantação local ou em servidores do Zabbix 7.2 utilizando `docker-compose`. Inclui os principais componentes: servidor Zabbix, frontend web, banco de dados PostgreSQL e agente Zabbix.

## 🚀 Tecnologias

- [Zabbix 7.2](https://www.zabbix.com/)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- PostgreSQL 15

## 📦 Estrutura dos serviços

- **postgres**: Banco de dados PostgreSQL usado pelo Zabbix.
- **zabbix-server**: Servidor principal de monitoramento.
- **zabbix-web**: Interface web baseada em Nginx + PHP.
- **zabbix-agent**: Agente Zabbix para monitorar o próprio host.

## 📁 Estrutura do projeto

```

zabbix/
├── docker-compose.yml
├── data/
│   └── postgres/             # Dados persistentes do banco
├── zbx\_env/
│   └── server/               # Configurações do Zabbix Server

````

## ⚙️ Como usar

1. Clone o repositório:

```bash
git clone https://github.com/marcosferreira/zabbix.git
cd zabbix
````

2. Crie os diretórios para persistência:

```bash
mkdir -p ./data/postgres ./zbx_env/server
```

3. Suba os containers:

```bash
docker-compose up -d
```

4. Acesse o frontend:

* URL: [http://localhost:8080](http://localhost:8080)
* Usuário padrão: `Admin`
* Senha padrão: `zabbix`

> ⚠️ Certifique-se de que as portas 8080 e 10051 estejam disponíveis no seu host.

## 📝 Personalização

* Para alterar configurações do Zabbix, edite os arquivos na pasta `zbx_env/server`.
* Para trocar o fuso horário, edite a variável `PHP_TZ` no `docker-compose.yml`.

## 📄 Licença

Este projeto está sob a licença [MIT](LICENSE).

---

Feito com 💻 por [Marcos Ferreira](https://github.com/marcosferreira)
