<div align="center">

[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://docs.python.org/3/)
[![Django](https://img.shields.io/badge/Django-4.2-092E20?style=for-the-badge&logo=django&logoColor=white)](https://docs.djangoproject.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/docs/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D?style=for-the-badge&logo=redis&logoColor=white)](https://redis.io/docs/)

*Full-stack web application with REST API, background tasks, and containerized deployment*

</div>

---

## Django Project Documentation

### Overview :

This project is a full-stack web application built with Django. 
Developed for KZ School to track Attendance and Other Updates  | The project has under gone various phases and this is the First sprint Repo made available as public.
It exposes a REST API, uses background workers for async tasks, and is deployed using Docker.

**Technology stack**

* Python 3.11
* Django 4.2
* PostgreSQL 15
* Redis 7
* Celery
* Docker

---

### Purpose of This Document :

This document is a technical reference intended to help developers:

* Understand the project structure
* Navigate the codebase
* Add or modify features safely
* Understand how components interact

---

### System Architecture :

```
Client
  ↓
Nginx
  ↓
Django (Gunicorn)
  ↓
PostgreSQL
  ↔
Redis
  ↓
Celery Workers
```

**Components**

* Nginx: request routing and static files
* Django: API, authentication, business rules
* PostgreSQL: persistent data storage
* Redis: caching and task queue
* Celery: background and scheduled jobs

---

### Project Structure :

```
project-root/
├── config/              # Settings, URLs, WSGI/ASGI
├── apps/                # Application modules
│   ├── users/
│   ├── orders/
│   └── payments/
├── frontend/            # Frontend code
├── static/              # Static assets
├── templates/           # HTML templates
├── tests/               # Test suite
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── manage.py
```

### Django App Structure :

```
apps/orders/
├── models.py
├── serializers.py
├── views.py / viewsets.py
├── urls.py
├── services.py
├── tasks.py
├── tests/
└── migrations/
```

---

## Design Conventions

### Business Logic :

Business logic lives in `services.py`.
Views should only coordinate input and output.

```python
def process_payment(user, amount):
    # validation
    # external calls
    # database updates
    return transaction
```

---

### Models :

Models define data structure only.
Avoid placing logic in models unless it is strictly data-related.

---

### API :

* Built using Django REST Framework
* Uses ViewSets and routers
* Base path: `/api/v1/`

**Authentication**

* JWT or session-based
* Header: `Authorization: Bearer <token>`

---

### Background Tasks :

* Long-running tasks are handled by Celery
* Tasks are defined in `tasks.py`
* Triggered using `.delay()` or `.apply_async()`

---

### Testing :

Tests are written using `pytest`.

```
Unit tests        (most)
Integration tests
E2E tests         (few)
```

Run tests:

```bash
pytest
pytest apps/orders/
pytest --cov=apps
```

---

### Local Development :

Start services:

```bash
docker-compose up
```

Common commands:

```bash
docker-compose run web python manage.py migrate
docker-compose run web python manage.py createsuperuser
docker-compose run web pytest
docker-compose run web python manage.py shell
```

---

### Deployment :

**Production setup**

* Multiple Django containers
* Managed PostgreSQL
* Redis for cache and queues
* Separate Celery workers

**Required environment variables**

```bash
DATABASE_URL=
REDIS_URL=
SECRET_KEY=
ALLOWED_HOSTS=
DEBUG=False
```
---

### Contribution Guidelines :

1. Create a feature branch
2. Write code and tests
3. Run tests and linters
4. Open a pull request
5. Merge after review

---

<div align="center">

[![GitHub](https://img.shields.io/badge/-Thousifibrahim-181717?style=flat-square&logo=github)](https://github.com/Thousifibrahim)
[![Email](https://img.shields.io/badge/-contact.thousif%2Bgithub@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:contact.thousif+github@gmail.com)
[![LinkedIn](https://img.shields.io/badge/-Thousif%20Ibrahim-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/smd-thousif-ibrahim-29050421b)

</div>
