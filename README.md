# Проект Yatube API

## Описание
Yatube API — это программный интерфейс для социальной сети Yatube. Проект предоставляет возможность взаимодействия с публикациями, комментариями, сообществами и подписками через REST API с использованием JWT-аутентификации.

Основные возможности API:
- Получение, создание, редактирование и удаление публикаций (`/api/v1/posts/`).
- Управление комментариями к публикациям (`/api/v1/posts/{post_id}/comments/`).
- Просмотр информации о сообществах (`/api/v1/groups/`).
- Управление подписками на авторов с поддержкой поиска (`/api/v1/follow/`).
- Аутентификация с помощью JWT-токенов (`/api/v1/jwt/`).

---

## Технологии
- Python 3.9+
- Django 3.2+
- Django REST Framework (DRF)
- Djoser & djangorestframework-simplejwt

---

## Установка и запуск проекта

1. Клонируйте репозиторий с проектом:
   ```bash
   git clone https://github.com/yandex-praktikum/api-final-yatube-ad.git
   ```

2. Перейдите в папку с проектом и создайте виртуальное окружение:
   ```bash
   cd api-final-yatube-ad/yatube_api
   python -m venv venv
   ```

3. Активируйте виртуальное окружение:
   - На Windows: `venv\Scripts\activate`
   - На macOS/Linux: `source venv/bin/activate`

4. Установите зависимости из файла `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```

5. Выполните миграции базы данных:
   ```bash
   python manage.py migrate
   ```

6. Запустите локальный сервер:
   ```bash
   python manage.py runserver
   ```

После запуска документация к API будет доступна по адресу:
`http://127.0.0.1:8000/redoc/`

---

## Примеры запросов к API

### Получение JWT-токена
**POST** `/api/v1/jwt/create/`
```json
{
    "username": "your_username",
    "password": "your_password"
}
```

### Получение списка публикаций
**GET** `/api/v1/posts/`
Пример ответа:
```json
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 1,
            "author": "username",
            "text": "Текст первой публикации",
            "pub_date": "2026-10-14T12:00:00Z",
            "image": null,
            "group": 1
        }
    ]
}
```

### Подписка на пользователя
**POST** `/api/v1/follow/`
*(Требуется передать заголовок `Authorization: Bearer <access_token>`)*
```json
{
    "following": "author_username"
}
```