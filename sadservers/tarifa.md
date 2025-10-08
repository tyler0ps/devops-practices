https://sadservers.com/newserver/tarifa

```bash
sed -i '/- frontend_network/a\      - backend_network' docker-compose.yml 
sed -i 's/81/80/' custom-nginx_1.conf
docker compose restart
```