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

#### To generate a token, access the Zabbix web interface and follow the steps.

<img width="232" height="111" alt="image" src="https://github.com/user-attachments/assets/0f00cea7-3223-414c-beca-7eba3e63717f" />

---
<img width="1910" height="570" alt="image" src="https://github.com/user-attachments/assets/b03a2fb8-7a82-41cd-8b91-3f14a3698c19" />

---
<img width="683" height="316" alt="image" src="https://github.com/user-attachments/assets/7f4da26d-27d8-4d2f-b65c-fc8a4abe9555" />

---
<img width="791" height="329" alt="image" src="https://github.com/user-attachments/assets/11ca0209-4c9b-4ea2-bf3c-81576af5364a" />

⚠️ Note: save this token before closing the screen.

---
```env
############################################
# Application login
############################################
APP_USER=YOUR_USERNAME
APP_PASS=YOUR_PASSWORD

############################################
# Zabbix (API)
# Tip: you can use the base URL (https://...),
# the backend automatically appends /api_jsonrpc.php
############################################
ZABBIX_URL=https://YOUR_ZABBIX_ADDRESS
ZABBIX_TOKEN=PASTE_YOUR_TOKEN_HERE

# Timeout (seconds) for Zabbix API calls (via proxy)
ZABBIX_TIMEOUT=15

############################################
# APPLICATION LOGS (PHP)
#
# LOG_LEVEL: controls the log "verbosity" of the application
# Options: debug | info | warn | error
# - debug: everything (use only for troubleshooting)
# - info : normal (recommended for production)
# - warn : only warnings/errors (quieter)
# - error: only critical errors
############################################
LOG_LEVEL=info

# LOG_TO_STDOUT: send logs to stdout/stderr (docker logs)
# Options: 1 (yes) | 0 (no)
# Recommended: 1
LOG_TO_STDOUT=1

# LOG_FILE: write logs to a file inside the container.
# Options:
# - empty (disable file logging): LOG_FILE=
# - path (e.g.: /var/log/app/app.log)
# Note: to persist logs, mount volume ./logs:/var/log/app
LOG_FILE=/var/log/app/app.log

############################################
# NGINX LOGS (web server)
#
# NGINX_ERROR_LOG_LEVEL:
# Common options: debug | info | notice | warn | error | crit | alert | emerg
# Recommended: warn
# - debug: VERY verbose (use temporarily)
# - warn : good for production
# - error: quieter
############################################
NGINX_ERROR_LOG_LEVEL=warn

# NGINX_ACCESS_LOG:
# Options:
# - /dev/stdout  (recommended: visible in docker logs)
# - off          (disable access log)
# - /var/log/nginx/access.log (file, if you mount a volume)
NGINX_ACCESS_LOG=/dev/stdout

# NGINX_ERROR_LOG:
# Options:
# - /dev/stderr  (recommended: visible in docker logs)
# - /var/log/nginx/error.log (file, if you mount a volume)
NGINX_ERROR_LOG=/dev/stderr
```

---

### 3. Inside the project directory, start the container with the command below:

```bash
docker compose up -d
```

### 4. Access via browser

- http://SERVER_IP:8000
- Log in using the credentials defined in `.env`

---

### ▶️ Step-by-step video
https://www.youtube.com/watch?v=G-NSQNW7GyU

### 📥 Download
- [Click here](https://github.com/serviceticst/relatorio-api-zabbix) 

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










