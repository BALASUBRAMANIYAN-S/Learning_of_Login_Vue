# Login and Register: Vue 3 + Django REST

A full-stack practice project with user registration and login. The backend is Django REST Framework with MySQL, and the frontend is Vue 3 with Vuetify.

## Features

- Register page and Login page in one screen (toggle between them)
- Form validation and error messages
- Login state kept in a Pinia store
- Home page with a logout button
- REST API for registration, login and profiles

## Tech Stack

| Part | Technology |
|---|---|
| Frontend | Vue 3, TypeScript, Vite, Vuetify 3, Pinia, Vue Router |
| Backend | Django, Django REST Framework, django-cors-headers |
| Database | MySQL (`django_db`) |

## Project Structure

```
├── backend/
│   ├── main/        # Django project settings and urls
│   ├── users/       # Register and login API
│   └── login/       # Profile model and API
└── frontend/
    └── src/
        ├── pages/   # Login.vue, homeSection.vue, index.vue
        ├── stores/  # auth.ts (Pinia)
        ├── utils/   # api.ts (fetch helper)
        └── router/
```

## API

Base URL: `http://127.0.0.1:8000/api/`

| Method | Endpoint | Body | Purpose |
|---|---|---|---|
| POST | `users/register/` | `username`, `email`, `password` | Create a user |
| POST | `users/login/` | `username`, `password` | Log in and return the user id |
| GET / POST | `profiles/` | `username`, `password` | List or create profiles |

## Getting Started

### Backend

```bash
cd backend
python -m venv .venv
.venv\Scripts\activate          # Windows (use source .venv/bin/activate on Linux/macOS)
pip install django djangorestframework django-cors-headers mysqlclient
```

1. Create a MySQL database named `django_db`.
2. Put your own MySQL user and password in the `DATABASES` setting in `main/settings.py`.
3. Run the migrations and start the server:

```bash
python manage.py migrate
python manage.py runserver
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Open the URL shown in the terminal (usually `http://localhost:5173`). The API address is set in `src/stores/auth.ts`.

## Notes

- Keep database passwords and the Django `SECRET_KEY` in environment variables, not in `settings.py`.
- The login endpoint currently returns a success message and the user id. The frontend is ready to store a token when the backend returns one (for example JWT).
- `CORS_ALLOW_ALL_ORIGINS = True` is for development only.
