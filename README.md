# zabbix-compose

Офіційна сторінка для завантаження та встановлення docker
[Docker Doks](https://docs.docker.com/engine/install/ubuntu/)

# Встановлення docker на ubuntu 20.04,20.10
```bash
sudo apt-get install apt-transport-https ca-certificates curl \
    gnupg lsb-release
	
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose

sudo usermod -aG docker $USER
```
# Встановлення Docker Compose
Зазвичай команда яку вводиш з оф сайту докера викачує найсвіжішу версію. Але перевірити наявність нової версії можна тут [Docker Compose GitHub](https://github.com/docker/compose/releases)
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/v2.15.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## Перед запуском сервера відредагуйте змінн compose файле під себе
```bash
POSTGRES_USER=zabbix
POSTGRES_PASSWORD=zabbix
POSTGRES_DB=zabbixNew
```

# Старт і зупинка сервера

## Старт
```bash
sudo docker-compose -f docker-compose-server-amd64.yaml up -d
```

Якщо захочете обнулити данні БД і підняти сервак заново але з чистою конфігурацією то треба видалити /var/lib/postgresql/data
```bash
sudo rm -rf /var/lib/postgresql/data
```

## Зупинка
```bash
sudo docker-compose -f docker-compose-server-amd64.yaml down
```

# Старт і зупинка proxy
## Старт
```bash
sudo docker-compose -f docker-compose-proxy-amd64.yaml up -d
```

## Зупинка
```bash
sudo docker-compose -f docker-compose-proxy-amd64.yaml down
```
