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
## Переменные окружения

Образ с Django считывает настройки из переменных окружения:

`SECRET_KEY` -- обязательная секретная настройка Django. Это соль для генерации хэшей. Значение может быть любым, важно лишь, чтобы оно никому не было известно. [Документация Django](https://docs.djangoproject.com/en/3.2/ref/settings/#secret-key).

`DEBUG` -- настройка Django для включения отладочного режима. Принимает значения `TRUE` или `FALSE`. [Документация Django](https://docs.djangoproject.com/en/3.2/ref/settings/#std:setting-DEBUG).

`ALLOWED_HOSTS` -- настройка Django со списком разрешённых адресов. Если запрос прилетит на другой адрес, то сайт ответит ошибкой 400. Можно перечислить несколько адресов через запятую, например `127.0.0.1,192.168.0.1,site.test`. [Документация Django](https://docs.djangoproject.com/en/3.2/ref/settings/#allowed-hosts).

`DATABASE_URL` -- адрес для подключения к базе данных PostgreSQL. Другие СУБД сайт не поддерживает. [Формат записи](https://github.com/jacobian/dj-database-url#url-schema).


## Удаление сессий
```
kubectl apply -f django_clearsessions_job.yaml
```

## Миграции

```
kubectl apply -f django_migrate_job.yaml
```

## Запуск postgres с помощью helm chart

- Установить [helm](https://github.com/helm/helm/releases)
- Не забудьте прописать путь до helm в системную переменную PATH
- Запустить release of postgresql chart
```
helm install my-release oci://registry-1.docker.io/bitnamicharts/postgresql
```

- При запуске вы увидите подробные инструкции, как подключиться к БД


