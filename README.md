## HW14
```
Был уствновлен docker
Запущен образ docker run hello-world
Изучено что:
```
1. Сама команда docker run = docker create + docker start + docker attach* (при добавлении -i)
>docker ps (показывает запущенные контейнеры ) | docker -a (показыввает все)

2. Команды: 
> docker start <u_container_id>
> docker attach <u_container_id>
```Позваляют запустить кокретный контейнер и потом присоединится к нему SSH```

3. А команда exec позволяет запускать внутри программы различный софт
> docker exec -it <u_container_id> bash
> docker inspect

4. Показывает информациюу о ресурсах образов и контейнерах в системе
> docker system df 

5. Убить процесс,а потом удалить из системы контейнер и образ можно с помощью команд:
> docker kill $(docker ps -q)
> docker rm $(docker ps -a -q)
> >docker rmi $(docker images -q)

## HW15

1. Создан новый проект в gcloud
2. Создал Docker-хост

```
docker-machine create --driver google \
--google-project docker-181710 \
--google-zone europe-west1-b \
--google-machine-type g1-small \
--google-machine-image $(gcloud compute images list --filter ubuntu-1604-lts --uri) \
docker-host
```
3. Добавил 4 файла:
> Dockerfile
> mongod.conf
> db_config
> start.sh

4. Произвёл сборку командой:
> docker build -t reddit:latest .
5. запустил контейнер
> docker run --name reddit -d --network=host reddit:latest
6. Открыл порт 9292
```
gcloud compute firewall-rules create reddit-app \
--allow tcp:9292 --priority=65534 \
--target-tags=docker-machine \
--description="Allow TCP connections" \
--direction=INGRESS
```
7. Зарегистрировался в "Docker hub"
8. Загрузил образ на docker hub
