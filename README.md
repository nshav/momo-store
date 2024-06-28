# Momo Store aka Пельменная №2

URL Momo Store: https://pelmeny-for.fun

## Requirments
- standalone server (based on ubuntu server for example) with internet access
- installed nginx, docker and docker-compose on this server

## Arcitecture
internet -> NGINX on standalone server -> wallaby-node -> momo-frontend -> momo-backend

## Deploying instruction
1. Copy these files to your home path (or anywhere you want) on the server:
   - docker-compose.yaml
   - frontend/default.conf
   - .env
2. Configure docker-compose.yaml, by adding path to your coppied default.conf
```bash
vim docker-compose.yaml
...
volumes:
  - "your_path/default.conf:/etc/nginx/conf.d/default.conf"
networks:
...
```
3. Configure your .env file. Add your WALLARM_API_TOKEN and WALLARM_API_HOST (you can create and find it in this instruction: https://docs.wallarm.com/admin-en/installation-docker-en/)
```bash
vim .env
```
4. Start docker-compose commad from path where docker-compose.yaml and .env are located
```bash
docker compose up -d
```
5. Wait for finishing executing
6. Configure your host NGINX. Add configuration momo-store to /etc/nginx/sites-avaliabl and replace server_name inside on yours. 
7. Create symlink to this file in directory /etc/nginx/sites-enabled
```bash
sudo ln -s /etc/nginx/sites-available/momo-store /etc/nginx/sites-enabled/
```
8. Restart your nginx
```bash
sudo systemctl restart nginx
```
9. Go to browser for checkin result.
10. If you have domain name, you can make certificate for using https:
```bash
sudo apt-get install certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```
