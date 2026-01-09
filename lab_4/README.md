# Django Tutorial - Lab 4

## Запуск проекта

1. Активировать виртуальное окружение:
```bash
source venv/bin/activate
```

2. Установить зависимости (если требуется):
```bash
pip install django
```

3. Применить миграции:
```bash
cd lab_4
python manage.py migrate
```

4. Создать суперпользователя (опционально):
```bash
python manage.py createsuperuser
```

5. Запустить сервер разработки:
```bash
python manage.py runserver
```

6. Открыть в браузере:
- Главная страница: http://127.0.0.1:8000/
- Создание опроса: http://127.0.0.1:8000/create/ (требуется авторизация)
- Регистрация: http://127.0.0.1:8000/accounts/register/
- Вход: http://127.0.0.1:8000/accounts/login/
- Админка: http://127.0.0.1:8000/admin/

## Тестирование

Запуск тестов:
```bash
python manage.py test polls
python manage.py test accounts
```

## Структура проекта

```
lab_4/
├── manage.py
├── db.sqlite3
├── mysite/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── polls/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── forms.py
│   ├── tests.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
│       ├── __init__.py
│       └── 0001_initial.py
├── accounts/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
│   ├── urls.py
│   └── migrations/
│       └── __init__.py
├── analytics/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── views.py
│   └── migrations/
│       └── __init__.py
└── templates/
    ├── polls/
    │   ├── base.html
    │   ├── index.html
    │   ├── create.html
    │   ├── detail.html
    │   └── results.html
    ├── accounts/
    │   └── register.html
    └── registration/
        └── login.html
```

## Основные функции

- **Просмотр опросов**: Все пользователи могут просматривать список опросов и голосовать
- **Создание опросов**: Только авторизованные пользователи могут создавать новые опросы
- **Регистрация**: Новые пользователи могут зарегистрироваться через форму регистрации
- **Авторизация**: Пользователи могут входить и выходить из системы
- **Связь с автором**: Каждый опрос связан с пользователем, который его создал
