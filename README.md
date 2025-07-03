# 🧠 Node-RED com Docker e Persistência de Dados

Este projeto executa o [Node-RED](https://nodered.org/) usando Docker, garantindo que os dados (fluxos, credenciais e configurações) sejam **persistidos mesmo após reinícios do sistema**.

---

## 🚀 Como usar

### 1. Clone ou crie a estrutura do projeto

```bash
mkdir node-red-project && cd node-red-project
mkdir data
```

### 2. Crie o arquivo `docker-compose.yml`

```yaml
version: '3.8'

services:
  nodered:
    image: nodered/node-red:latest
    container_name: nodered
    restart: unless-stopped
    ports:
      - "1880:1880"
    volumes:
      - ./data:/data
    environment:
      - TZ=America/Sao_Paulo
```

### 3. Suba o contêiner

```bash
docker compose up -d
```

### 4. Acesse o Node-RED

Abra no navegador:

```
http://localhost:1880
```

---

## 💾 Persistência de Dados

A pasta `./data` no seu sistema hospedeiro está mapeada para o diretório `/data` dentro do contêiner, que é onde o Node-RED armazena:

- `flows.json` – Seus fluxos.
- `flows_cred.json` – Suas credenciais (criptografadas).
- `settings.js` – Configurações do ambiente.

✅ Isso garante que nenhum dado será perdido ao reiniciar o contêiner ou o sistema.

---

## 🔄 Reinicialização automática

O serviço foi configurado com:

```yaml
restart: unless-stopped
```

Isso faz com que o Node-RED reinicie automaticamente se travar ou se o sistema reiniciar.

---

## 📦 Backup dos Dados

Você pode fazer backup apenas copiando a pasta `data`:

```bash
cp -r data backup-node-red
```


recriar container:
```bash
 docker-compose up --force-recreate
 ```
 
---

## 📌 Requisitos

- Docker
- Docker Compose

---

## 🛠️ Personalização

Quer adicionar autenticação, temas, pacotes extras ou usar SSL (HTTPS)? Fique à vontade para abrir uma _issue_ ou modificar a configuração conforme suas necessidades.

---

## 🧑‍💻 Autor

**Rafael Conrado**  
Projeto voltado para automações, integrações e desenvolvimento de fluxos com Node-RED.

---