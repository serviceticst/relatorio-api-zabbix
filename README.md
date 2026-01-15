## <img src="https://flagcdn.com/w40/br.png" width="40">  🧩 Imagem docker com relatório do [Zabbix](https://www.zabbix.com) via API.
### 1. Escolha um diretório dentro do seu servidor, crie ou [baixe](https://github.com/serviceticst/relatorio-api-zabbix) o arquivo `docker-compose.yml` conforme modelo abaixo. Se preferir, altere a porta 8000 de acordo com a sua necessidade.

```yaml
services:
  relatorio-zabbix:
    image: ghcr.io/serviceticst/relatorio-api-zabbix:1.0.0
    container_name: relatorio-zabbix
    ports:
      - "8000:80"
    environment:
      # Login da aplicação
      APP_USER: "${APP_USER}"
      APP_PASS: "${APP_PASS}"

      # Zabbix
      ZABBIX_URL: "${ZABBIX_URL}"
      ZABBIX_TOKEN: "${ZABBIX_TOKEN}"
      ZABBIX_TIMEOUT: "${ZABBIX_TIMEOUT}"

      # Logs da aplicação (PHP)
      LOG_LEVEL: "${LOG_LEVEL}"          
      LOG_TO_STDOUT: "${LOG_TO_STDOUT}"     
      LOG_FILE: "${LOG_FILE}"

      # Logs do Nginx
      NGINX_ERROR_LOG_LEVEL: "${NGINX_ERROR_LOG_LEVEL}"
      NGINX_ACCESS_LOG: "${NGINX_ACCESS_LOG}"
      NGINX_ERROR_LOG: "${NGINX_ERROR_LOG}"

    volumes:
      - ./logs:/var/log/app
    restart: unless-stopped
    healthcheck:
      test: ["CMD-SHELL", "curl -fsS http://localhost/healthz || exit 1"]
      interval: 10s
      timeout: 3s
      retries: 5

```
---

### 2. Crie ou [baixe](https://github.com/serviceticst/relatorio-api-zabbix) no mesmo diretório o arquivo `.env` e ajuste as variáveis abaixo conforme o seu ambiente:

```env
APP_USER=seu_usuario
APP_PASS=sua_senha
ZABBIX_URL=https://zabbix.exemplo.com
ZABBIX_TOKEN=seu_token_aqui
```
#### ⚠️ Atenção aos comentários no arquivo `.env`!
---

### 3. Para gerar um token, acesse a interface web do zabbix e siga o passo a passo abaixo:


<img width="232" height="111" alt="image" src="https://github.com/user-attachments/assets/0f00cea7-3223-414c-beca-7eba3e63717f" />

---
<img width="1910" height="570" alt="image" src="https://github.com/user-attachments/assets/b03a2fb8-7a82-41cd-8b91-3f14a3698c19" />

---
<img width="683" height="316" alt="image" src="https://github.com/user-attachments/assets/7f4da26d-27d8-4d2f-b65c-fc8a4abe9555" />

---
<img width="791" height="329" alt="image" src="https://github.com/user-attachments/assets/11ca0209-4c9b-4ea2-bf3c-81576af5364a" />

#### ⚠️ Observação: Salve esse token antes de fechar a tela.
---

```env
############################################
# Login da aplicação 
############################################
APP_USER=admin
APP_PASS=admin123

############################################
# Zabbix (API)
# Dica: pode ser a base (https://...),
# o backend completa com /api_jsonrpc.php automaticamente
############################################
ZABBIX_URL=https://ENDERECO_ZABBIX_AQUI
ZABBIX_TOKEN=COLE_SEU_TOKEN_AQUI
# Timeout (segundos) para chamadas ao Zabbix via proxy
ZABBIX_TIMEOUT=15

############################################
# LOGS DA APLICAÇÃO (PHP)
#
# LOG_LEVEL: controla a "verbosidade" do log do app
# Opções: debug | info | warn | error
# - debug: tudo (usar só para troubleshooting)
# - info : normal (recomendado em produção)
# - warn : somente alertas/erros (mais silencioso)
# - error: somente erros graves
############################################
LOG_LEVEL=info

# LOG_TO_STDOUT: manda logs para stdout/stderr (docker logs)
# Opções: 1 (sim) | 0 (não)
# Recomendado: 1
LOG_TO_STDOUT=1

# LOG_FILE: grava logs em arquivo dentro do container.
# Opções:
# - vazio (desliga log em arquivo): LOG_FILE=
# - caminho (ex.: /var/log/app/app.log)
# Observação: para persistir, monte volume ./logs:/var/log/app
LOG_FILE=/var/log/app/app.log

############################################
# LOGS DO NGINX (servidor web)
#
# NGINX_ERROR_LOG_LEVEL:
# Opções comuns: debug | info | notice | warn | error | crit | alert | emerg
# Recomendado: warn
# - debug: MUITO verboso (usar temporariamente)
# - warn : bom para produção
# - error: mais silencioso
############################################
NGINX_ERROR_LOG_LEVEL=warn

# NGINX_ACCESS_LOG:
# Opções:
# - /dev/stdout  (recomendado: aparece em docker logs)
# - off          (desliga access log)
# - /var/log/nginx/access.log (em arquivo, se você montar volume)
NGINX_ACCESS_LOG=/dev/stdout

# NGINX_ERROR_LOG:
# Opções:
# - /dev/stderr  (recomendado: aparece em docker logs)
# - /var/log/nginx/error.log (em arquivo, se montar volume)
NGINX_ERROR_LOG=/dev/stderr
```
---

### 4. Dentro do diretório, suba o contêiner com o comando abaixo: 

```bash
docker compose up -d
```
---
### 5. Acesse pelo navegador

- http://IP_DO_SERVIDOR:8000

- Logue com o usuário e senha definido nas variáveis
```env
APP_USER=seu_usuario
APP_PASS=sua_senha
```

- - - - - - - -


### ▶️ Passo a Passo
- Para assistir ao tutorial completo:
[Clique aqui](https://www.youtube.com/watch?v=G-NSQNW7GyU)

### 📥 Download
- [Clique aqui](https://github.com/serviceticst/glpi/releases/download/10.0.0/GLPI_10_ORACLE_LINUX_8.sh) 

### ⚙️ Funcionalidades
- Relatório prático do zabbix
- Exportação em PDF


***

## <img src="https://flagcdn.com/w40/us.png" width="40">  🧩 Docker Image with Zabbix Report via API

### 1. Choose a directory on your server and create or download the `docker-compose.yml` file according to the example below.
If needed, change port `8000` to suit your environment.

```yaml
services:
  zabbix-report:
    image: ghcr.io/serviceticst/relatorio-api-zabbix:1.0.0
    container_name: zabbix-report
    ports:
      - "8000:80"
    environment:
      # Application login
      APP_USER: "${APP_USER}"
      APP_PASS: "${APP_PASS}"

      # Zabbix
      ZABBIX_URL: "${ZABBIX_URL}"
      ZABBIX_TOKEN: "${ZABBIX_TOKEN}"
      ZABBIX_TIMEOUT: "${ZABBIX_TIMEOUT}"

      # Application logs (PHP)
      LOG_LEVEL: "${LOG_LEVEL}"
      LOG_TO_STDOUT: "${LOG_TO_STDOUT}"
      LOG_FILE: "${LOG_FILE}"

      # Nginx logs
      NGINX_ERROR_LOG_LEVEL: "${NGINX_ERROR_LOG_LEVEL}"
      NGINX_ACCESS_LOG: "${NGINX_ACCESS_LOG}"
      NGINX_ERROR_LOG: "${NGINX_ERROR_LOG}"

    volumes:
      - ./logs:/var/log/app
    restart: unless-stopped
    healthcheck:
      test: ["CMD-SHELL", "curl -fsS http://localhost/healthz || exit 1"]
      interval: 10s
      timeout: 3s
      retries: 5
```

---

### 2. Create the `.env` file in the same directory and adjust the variables according to your environment:

```env
APP_USER=your_user
APP_PASS=your_password
ZABBIX_URL=https://zabbix.example.com
ZABBIX_TOKEN=your_token_here
```

⚠️ Pay attention to the comments inside the `.env` file.

---

### 3. To generate a token, access the Zabbix web interface and follow the steps.

⚠️ Note: save this token before closing the screen.

---

### 4. Inside the project directory, start the container:

```bash
docker compose up -d
```

---

### 5. Access via browser

- http://SERVER_IP:8000

- Log in using the credentials defined in `.env`

---

### ▶️ Step-by-step video
https://www.youtube.com/watch?v=G-NSQNW7GyU

### ⚙️ Features
- Zabbix report generation
- PDF export

***

### Desenvolvido por: Service TIC Soluções Tecnológicas (Developed by: Service TIC Technological Solutions)

- [![E-mail](https://img.icons8.com/ios-filled/16/ffffff/mail.png)](mailto:contato@servicetic.com.br) **E-mail**: [contato@servicetic.com.br](mailto:contato@servicetic.com.br)
- [![Website](https://img.icons8.com/ios-filled/16/ffffff/domain.png)](http://www.servicetic.com.br) **Site**: [www.servicetic.com.br](http://www.servicetic.com.br)
- [![LinkedIn](https://img.icons8.com/ios-filled/16/ffffff/linkedin-circled.png)](https://www.linkedin.com/company/serviceticst) **LinkedIn**: [@serviceticst](https://www.linkedin.com/company/serviceticst)
- [![Instagram](https://img.icons8.com/ios-filled/16/ffffff/instagram-new.png)](https://www.instagram.com/serviceticst) **Instagram**: [@serviceticst](https://www.instagram.com/serviceticst)
- [![Facebook](https://img.icons8.com/ios-filled/16/ffffff/facebook-new.png)](https://www.facebook.com/serviceticst) **Facebook**: [@serviceticst](https://www.facebook.com/serviceticst)
- [![X](https://img.icons8.com/ios-filled/16/ffffff/x.png)](https://x.com/serviceticst) **Twitter**: [@serviceticst](https://x.com/serviceticst)
- [![YouTube](https://img.icons8.com/ios-filled/16/ffffff/youtube-squared.png)](https://youtube.com/c/serviceticst) **YouTube**: [@serviceticst](https://youtube.com/c/serviceticst)
- [![WhatsApp](https://img.icons8.com/ios-filled/16/ffffff/whatsapp.png)](https://whatsapp.com/channel/0029VaAkV3P59PwXAiDepu3N) **WhatsApp Channel**: [Clique aqui](https://whatsapp.com/channel/0029VaAkV3P59PwXAiDepu3N)

[![image](https://github.com/user-attachments/assets/17192a13-f0b6-4531-add0-99c7f46c24b0)](https://servicetic.com.br/links/)










