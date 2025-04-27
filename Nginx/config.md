# Guia Rápido: Configuração de Nginx + SSL Let's Encrypt

##  1. Instalação do Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

##  2. Configuração Básica do Nginx

Criar ou editar um arquivo de configuração para seu site em `/etc/nginx/sites-available/default`:

```nginx
server {
    listen 80;
    server_name SEUDOMINIO.com www.SEUDOMINIO.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

Verifique a configuração:

```bash
sudo nginx -t
```

E reinicie o Nginx:

```bash
sudo systemctl restart nginx
```

##  3. Instalação do Certbot + Plugin Nginx

```bash
sudo apt install certbot python3-certbot-nginx -y
```

##  4. Geração do Certificado SSL

Execute o Certbot:

```bash
sudo certbot --nginx
```

- Informe seu e-mail.
- Aceite os termos.
- Selecione os domínios a proteger.
- Escolha redirecionar HTTP para HTTPS (opção recomendada).

##  5. Testar o SSL

Verifique o status:

```bash
curl -I https://SEUDOMINIO.com
```

Deve retornar `HTTP/2 200` ou `HTTP/1.1 200 OK`.

##  6. Renovação Automática (Testar)

Certbot já configura um cron job para renovação automática. Teste com:

```bash
sudo certbot renew --dry-run
```

##  7. Modelo de Nginx otimizado

```nginx
server {
    listen 80;
    server_name SEUDOMINIO.com www.SEUDOMINIO.com;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl;
    server_name SEUDOMINIO.com www.SEUDOMINIO.com;

    ssl_certificate /etc/letsencrypt/live/SEUDOMINIO.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/SEUDOMINIO.com/privkey.pem;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

---

# Observações Finais

- Certifique-se que as portas **80** e **443** estão liberadas no Security Group da AWS.
- Sempre teste configurações Nginx com `nginx -t` antes de reiniciar.
- Certificados Let's Encrypt são válidos por 90 dias, mas o Certbot automatiza a renovação.

---