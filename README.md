# Momo Store aka Пельменная №2

URL Momo Store: https://pelmeny-for.fun

## Requirments
- standalone server (based on ubuntu server for example) with internet access
- installed nginx, docker and docker-compose on this server

## Arcitecture
![alt text](https://storage.yandexcloud.net/momo-store-wallarm/architectire.jpg)

## Deploying instruction
1. Connect via ssh to your server.
2. Copy these files to your home path (or anywhere you want) on the server:
   - docker-compose.yaml
   - frontend/default.conf
   - .env
3. Configure docker-compose.yaml, by adding path to your coppied default.conf
```bash
vim docker-compose.yaml
...
volumes:
  - "your_path/default.conf:/etc/nginx/conf.d/default.conf"
networks:
...
```
4. Configure your .env file. Add your WALLARM_API_TOKEN and WALLARM_API_HOST (you can create and find it in this instruction: https://docs.wallarm.com/admin-en/installation-docker-en/)
```bash
vim .env
```
5. Start docker-compose command from path where docker-compose.yaml and .env are located:
```bash
docker compose up -d
```
6. Wait for finishing executing. You wil see names of three containers with status "Started"
7. Configure your host NGINX. Add configuration momo-store to /etc/nginx/sites-avaliable and replace server_name inside on your domain name. 
8. Create symlink to this file in directory /etc/nginx/sites-enabled:
```bash
sudo ln -s /etc/nginx/sites-available/momo-store /etc/nginx/sites-enabled/
```
9. Restart your nginx:
```bash
sudo systemctl restart nginx
```
10. If you have domain name, you can make certificate for using https:
```bash
sudo apt-get install certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```
11. Go to web browser for checking result.
