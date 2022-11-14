# API для Yatube
## Описание
В проекте реализован REST API для Yatube, который позволяет получать 
информацию о постах, комментариях, группах и авторах, а так же 
создавать и редактировать свои записи и комментарии, подписываться
на новых авторов, и просматривать список подписок.

Установка
Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:

```
git clone https://github.com/AlexeyTikhonchuk/api_final_yatube.git
```

```
cd api_final_yatube
```

Cоздать и активировать виртуальное окружение:

```
python -m venv env
```

```
source env/bin/activate
```

```
python -m pip install --upgrade pip
```

Установить зависимости из файла requirements.txt:

```
pip install -r requirements.txt
```

Выполнить миграции:

```
python manage.py migrate
```

Запустить проект:

```
python manage.py runserver
```

##Примеры запросов
###Получение списка публикаций
Для получения списка всех публикаций необходимо отправить 
Get-запрос на адрес `http://127.0.0.1:8000/api/v1/posts/`.
При помощи параметров `limit` и `offset` можно настроить размер
и область выдачи

Пример ответа:
```
[
    {
        "id": 1,
        "author": "AlexTheSecond",
        "text": "SomeText",
        "pub_date": "2022-08-07T21:36:52.908182Z",
        "image": null,
        "group": null
    },
    {
        "id": 2,
        "author": "AlexTheSecond",
        "text": "SomeNewText",
        "pub_date": "2022-08-07T21:37:05.442929Z",
        "image": null,
        "group": null
    }
]
```

###Добавление публикации
Для добавления новой публикации необходимо отправить POST-запрос
на адрес `http://127.0.0.1:8000/api/v1/posts/` в JSON формате:

```
{
    "text": "Ваш текст",
    "group": 1
} 
```
Пример ответа:
```
    {
        "id": 3,
        "author": "AlexTheSecond",
        "text": "Ваш текст",
        "pub_date": "2022-08-07T21:37:05.442929Z",
        "image": null,
        "group": 1
    }
```
###Добавление комментария
Для добавления новой публикации необходимо отправить POST-запрос
на адрес `http://127.0.0.1:8000/api/v1/posts/4/comments/` в JSON формате:
```
{
    "text": "текст комментария"
} 
```
Пример ответа:
```
{
    "id": 1,
    "author": "AlexTheSecond",
    "post": 1,
    "text": "текст комментария",
    "created": "2022-08-07T21:37:05.442929Z"
} 
```
###Добавление подписки
Для добавления новой подписки необходимо отправить POST-запрос
на адрес `http://127.0.0.1:8000/api/v1/follow/` в JSON формате с именем автора, 
на которого хотите подписаться:
```
{
    "following": "name"
} 
```
Пример ответа:
```
{
    "id": 1,
    "user": "AlexTheSecond",
    "following": "name",
} 
```
Для GET-запроса доступен поиск автора среди подписок.
##Технологии
- python
- django
## Автор
https://github.com/AlexeyTikhonchuk
