![Workflow Status](https://github.com/ElenaGruzintseva/kittygram_final/actions/workflows/main.yml/badge.svg)

# Kittygram

Kittygram — это сервис для хранения информации о котиках. Здесь вы можете добавлять, редактировать и удалять информацию о своих котиках. Каждый котик имеет фото, имя, возраст и достижения. Чужих котиков удалять нельзя.

## Стек технологий
 - Django
 - DRF
 - djoser
 - PyYAML
 - Nginx
 - Docker Compose
 - GitHub Actions

### Как развернуть проект не используя workflow

Убедитесь, что на вашем компьютере установлены Docker и Docker Compose.

Клонируйте репозиторий:

```
git clone https://github.com/ElenaGruzintseva/kittygram_final.git
cd kittygram_final
```

Создайте файл .env в корне проекта и добавьте необходимые переменные окружения. Пример:

```
POSTGRES_USER=user
POSTGRES_PASSWORD=password
POSTGRES_DB=db
DB_HOST=db
DB_PORT=5432
SECRET_KEY=your_generated_secret_key_here
DEBUG=False
ALLOWED_HOSTS=127.0.0.1,localhost
USE_SQLITE=True(Если хотите использовать SQLite вместо PostgreSQL)
```

Запустите Docker Compose для создания и запуска контейнеров:

```
docker-compose -f docker-compose.production.yml up -d
```

Примените миграции базы данных и соберите статические файлы:

```
docker-compose -f docker-compose.production.yml exec backend python manage.py migrate
docker-compose -f docker-compose.production.yml exec backend python manage.py collectstatic --noinput
```


### Для автоматизации развертывания и тестирования проекта можно использовать GitHub Actions

Ознакомьтесь с файлом конфигурации GitHub Actions (kittygram_workflow.yml), который содержит шаги для тестирования и сборки.

Добавьте секреты в репозиторий:

```
DOCKER_PASSWORD - пароль от Docker Hub
DOCKER_USERNAME - имя пользователя Docker Hub
HOST - ip сервера
USER - имя пользователя сервера
SSH_KEY - ключ ssh для доступа к удаленному серверу
SSH_PASSPHRASE - пароль ssh
TELEGRAM_TO - id пользователя TELEGRAM
TELEGRAM_TOKEN - TELEGRAM токен для отправки сообщений
```

При каждом пуше в ветку main GitHub Actions автоматически запустит тесты, соберет Docker-образы, и развернёт проект на сервере.

При каждом пуше в любую другую ветку GitHub Actions только запустит тесты.

После успешного выполнения workflow, образы будут опубликованы на DockerHub,
а в Telegram будут отправлены сообщения об успешном деплое.


### [ElenaGruzintseva](https://github.com/ElenaGruzintseva)