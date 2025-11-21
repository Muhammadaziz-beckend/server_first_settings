# 1. Обновление сервера

```bash
sudo apt update && sudo apt upgrade -y
```

# 2. Установка Nginx

```bash
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
```

## Проверка статуса:

```
systemctl status nginx
```

# 3. Установка Docker

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

## Добавляем себя в группу docker, чтобы не писать sudo:

```
sudo usermod -aG docker $USER
```

## Проверка:

```
docker --version
docker ps
```

# 4. Установка Docker Compose

```
sudo apt install docker-compose-plugin -y
```

## Проверка:

```
docker compose version
```

# 5. Проверка занятых портов (очень важная штука!) Показать список всех портов:

```
sudo lsof -i -P -n | grep LISTEN
```

### Проверить конкретный порт:

```
sudo lsof -i :<port>
sudo lsof -i :8000
```
