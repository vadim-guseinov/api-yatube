<div align="center">

# 📝 Yatube API (Token Auth)

**REST API блог-платформы на Django REST Framework: посты, группы и комментарии с аутентификацией по токену**

![Python](https://img.shields.io/badge/Python-3.12-3776AB?logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-5.1-092E20?logo=django&logoColor=white)
![DRF](https://img.shields.io/badge/DRF-ViewSets-A30000?logo=django&logoColor=white)
![Tests](https://img.shields.io/badge/pytest-49%2F49_passed-2ea44f?logo=pytest&logoColor=white)

</div>

> Первая версия API Yatube. Расширенная версия с JWT, подписками и пагинацией — **[api-final-yatube](https://github.com/JuliaDJ1/api-final-yatube)**.

## О проекте

API для социальной сети Yatube: пользователи публикуют посты, объединяют их в группы и обсуждают в комментариях. Доступ — только для аутентифицированных пользователей, изменять и удалять контент может только его автор.

## Возможности

- Аутентификация по токену (`rest_framework.authtoken`).
- Посты — полный CRUD; комментарии — вложенный ресурс `/posts/{id}/comments/`; группы — только чтение.
- Собственный permission `IsAuthorOrReadOnly`: чужой контент можно только читать.
- **49 из 49 автотестов** pytest проходят.

## Стек

Python 3.12 · Django 5.1 · Django REST Framework · TokenAuthentication · SQLite · pytest

## Запуск

**Требования:** Python 3.10+ (проверено на 3.12).

```bash
git clone https://github.com/JuliaDJ1/api-yatube.git
cd api-yatube
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

cd yatube_api
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

### Тесты

```bash
pytest          # из корня репозитория
```

## Примеры запросов

```bash
# получить токен
curl -X POST http://127.0.0.1:8000/api/v1/api-token-auth/ \
  -d "username=user&password=strongpassword"
# {"token": "<token>"}

# создать пост
curl -X POST http://127.0.0.1:8000/api/v1/posts/ \
  -H "Authorization: Token <token>" \
  -H "Content-Type: application/json" \
  -d '{"text": "Привет, Yatube!", "group": 1}'

# комментарии к посту
curl http://127.0.0.1:8000/api/v1/posts/1/comments/ -H "Authorization: Token <token>"
```

## Автор

**Вадим Гусейнов** — Python-разработчик (Backend) · [Telegram](https://t.me/eviliing)
