# Описание

## Модели
1. Users
   1. fullname
   2. username
   3. password (hash)
   4. birthday (nullable)
   5. bio
   6. signup_at (не принимается а заполняется текщим временем)
   7. last_action (автообновление после каждого действия)
   8. avatar (строка обозначающая путь в файловой системе) 

2. Posts
   1. photo
   2. content
   3. created_at
   4. author_id

3. Likes_Posts
   1. post_id
   2. user_id

4. Comments
   1. post_id
   2. comment_parent_id
   3. user_id
   4. content

5. Subscribes
   1. author_id
   2. subscriber_id
   
Инструменты:

Python
FastAPI
SQLAlchemy
Текст с описанием картинки
Grok задаем порт ,который будет идти на движок nginx. Если в адресе есть ручка с API, то nginx отправляет запрос на backend, если название домена без ручек, то на frontend

Установка окружения poetry:

poetry shell
poetry install
Инициализируем репозиторий:

git init
Установка pre-commit для чистоты ,наглядности и понятности кода:

pre-commit install
Добавляем вэб сервер uvicorn:

poetry add uvicorn
Папка src будет главной папкой проекта, из которой будем делать все запуски.
В файле app.py создаем пробный запуск приложения:

from fastapi import FastAPI

app = FastAPI()


@app.get("/")
def read_root():
    return {"Hello": "World"}
Описание API
Регистрация пользователя
URL: /users/signup/
Метод: POST
Описание: Регистрирует нового пользователя в системе.
Тело запроса (JSON):
{
  "username": "test_user",
  "password": "1234",
  "fullname": "Ivan Ivanov ",
  "email": "ivan@test.com",
  "avatar": "http://test.com/avatar.jpg"
}
Пример успешного ответа:
{
  "id": 1,
  "username": "test_user",
  "fullname": "Ivan Ivanov",
  "email": "ivan@test.com",
  "avatar": "http://test.com/avatar.jpg"
}
Пример запроса с ошибкой:
{
  "detail": "Username already taken"
}
Аутентификация пользователя:
URL: /users/login/
Метод: POST
Описание: маршрут /token, который принимает данные формы запроса с именем пользователя и паролем, аутентифицирует пользователя с помощью функции authenticate_user, и если пользователь успешно аутентифицирован, генерирует и возвращает токен доступа.
Тело запроса (form-data):
Текст с описанием картинки

Пример успешного ответа:
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJSdXNsYW4iLCJleHAiOjE3MTY3NTg0Nzl9.ma2sbuK0CToG75fu8SqRUWwtAPedOQqMTxnrHcHNQMw",
    "token_type": "bearer"
}
Пример запроса с ошибкой:
{
  "detail": "Incorrect username or password"
}
