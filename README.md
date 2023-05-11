# CI и CD проекта YaMDB

![workflow status](https://github.com/maximuz2004/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)
[![Python](https://camo.githubusercontent.com/a00abd8cea4105fa1cad91f7235d11206b492f51afeb9b23a25d04e8f36935e3/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f507974686f6e2d4646443433423f7374796c653d666f722d7468652d6261646765266c6f676f3d707974686f6e266c6f676f436f6c6f723d626c7565)](https://www.python.org/)  [![Django](https://camo.githubusercontent.com/dd7f390cf162d4b963b26215e6cd4373282ebe20caccfd4ef479798c2b590e38/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446a616e676f2d3039324532303f7374796c653d666f722d7468652d6261646765266c6f676f3d646a616e676f266c6f676f436f6c6f723d677265656e)](https://www.djangoproject.com/) 
[![Django REST Framework](https://camo.githubusercontent.com/4a6c6851aab9b0042c0baaea2c61993ea052cff554d8a3d42cd51d67d304d452/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f646a616e676f253230726573742d6666313730393f7374796c653d666f722d7468652d6261646765266c6f676f3d646a616e676f266c6f676f436f6c6f723d7768697465)](https://www.django-rest-framework.org/)
[![Docker](https://camo.githubusercontent.com/63350538fde994bc287ccd4908809301e157980e6564bf78d2c5cec22c0a5914/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f636b65722d3243413545303f7374796c653d666f722d7468652d6261646765266c6f676f3d646f636b6572266c6f676f436f6c6f723d7768697465)](https://www.docker.com/)
[![Nginx](https://camo.githubusercontent.com/6f06f5c158e5ff38ad3c8441bfcb44886de846850c3bef6b465901312242dd19/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f4e67696e782d3030393633393f7374796c653d666f722d7468652d6261646765266c6f676f3d6e67696e78266c6f676f436f6c6f723d7768697465)](https://nginx.org/ru/)

### Описание
Проект YaMDb собирает **отзывы** пользователей на **произведения**. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Произведения делятся на **категории**, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).

Произведению может быть присвоен **жанр** из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»).

Добавлять произведения, категории и жанры может только администратор..

Основная задача проекта - предоставить удобный и простой способ для создания сторонних клиентов, в том числе мобильных приложений, с помощью которых пользователи смогут взаимодействовать со всеми функциями Yatube.
Аутентификация пользователей реализована по стандарту **JWT**.
### Как запустить проект:
1.  Клонируйте репозиторий:
```
git@github.com:Maximuz2004/yamdb_final.git
```
2.  Перейдите в директорию проекта. Создайте и активируйте виртуальное окрудение. Установите все зависимости:
```
python -m venv venv
source venv/bin/activate
python -m pip install --upgrade pip
pip install -r api_yamdb/requirements.txt

```
3. Запустите тесты. Проверьте, что они все прошли. 
```
pytest
```

4. Настройка удаленного сервера:

    1. Войдите на свой удаленный сервер. 
    2. Остановите службу nginx:
   ```
    sudo systemctl stop nginx
   ```
   3. Установите docker:
   ```
   sudo apt install docker.io
   ```
   4. Установите doker-compose согласно официальной [документации](https://docs.docker.com/compose/install/)

5. Скопируйте файлы docker-compose.yaml и nginx/default.conf из вашего проекта на сервер в home/<ваш_username>/docker-compose.yaml и home/<ваш_username>/nginx/default.conf соответственно.

    В файле ```nginx/default.conf ``` укажите ip-адрес вашего сервера

6. Добавьте в Secrets GitHub Actions переменные окружения для работы базы данных и всего остального:
```
ALLOWED_HOSTS - список допустимых хостов, которые могут обращаться к приложению
DB_ENGINE=django.db.backends.postgresql
DB_NAME=*имя базы данных*
POSTGRES_USER=*логин для подключения к базе данных*
POSTGRES_PASSWORD=*пароль для подключения к БД*
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
SECRET_KEY=*секретный ключ Джанго*
HOST - ip-адрес вашего сервера
USER - пользователь удаленного сервера
SSH_KEY - приватный ssh-ключ (публичный должен быть на сервере)
DOCKER_USERNAME - ваш ник на https://hub.docker.com/
DOCKER_PASSWORD - ваш пароль на DockerHub
TELEGRAM_TO - Ваше id в Телеграмме
TELEGRAM_TOKEN - токен вашего бота в Телеграмме
```
7. Запустите проект на сервере:
```
sudo docker-compose up -d
```

Создайте суперпользователя:
```
sudo docker-compose exec web python manage.py createsuperuser
```
или:

```
sudo docker-compose exec web python manage.py loaddata static/fixtures.json
```

Подробную документацию проекта вы можете посмотреть по [ссылке](https://yayatube.ddns.net/redoc/).

Проект доступен по адресу: https://yayatube.ddns.net/redoc/


## Авторы.
[Антон Киреев](https://github.com/AntiANT8406). Управление пользователями: система регистрации и аутентификации, права доступа, работа с токеном, система подтверждения e-mail.

[Михаил Кочетков](https://github.com/MikhailKochetkov). Отзывы, комментарии и рейтинги произведений: модели и view, эндпойнты для них.

[Максим Титов](https://github.com/Maximuz2004). 
Категории, жанры и произведения: модели, view и эндпойнты для них.

