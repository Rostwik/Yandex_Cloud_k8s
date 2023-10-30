# Django site

Докеризированный сайт на Django для экспериментов с Yandex Cloud.

## Собрать образ и залить в Docker Hub

- [Установите Docker](https://www.docker.com/)
- Перейлите в папку 'backend_main_django'
```commandline
cd backend_main_django
```
- Соберите образ локально
```
docker build -t dj_app_y8c .
```
- Залогиньтесь в Docker Hub
```commandline
docker login
```
- Создайте репозиторий в [Docker Hub](https://hub.docker.com/)
- Переименовать образ в соответствии с названием репозитория
```commandline
docker tag dj_app_y8c:latest rostwik/dj_app_y8c:main
```
- Загрузить новый образ в репозиторий Docker Hub
```commandline
docker push rostwik/dj_app_y8c:main
```
## Разворачиваем приложение

```
kubectl apply -f configmap.yaml
```
```
kubectl apply -f django_deploy.yaml
```

Если данные в configmap.yaml изменились необходимо выполнить следующие команды:
```
kubectl apply -f configmap.yaml
```
```
kubectl rollout restart deployment django-deployment
```

## Удаление сессий
```
kubectl apply -f django_clearsessions_job.yaml
```

## Миграции

```
kubectl apply -f django_migrate_job.yaml
```
## Пример сайта

Сайт доступен по [https://edu-dreamy-goodall.sirius-k8s.dvmn.org/](https://edu-dreamy-goodall.sirius-k8s.dvmn.org/) 