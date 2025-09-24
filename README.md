# Learning log (Django project)

![Made with Python](https://img.shields.io/badge/Made%20with-Python-3776AB?logo=python&logoColor=white)  ![Framework Django](https://img.shields.io/badge/Framework-Django-092E20?logo=django&logoColor=white)  ![Deployed on Heroku](https://img.shields.io/badge/Deployed%20on-Heroku-430098?logo=heroku&logoColor=white)  ![Database PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-336791?logo=postgresql&logoColor=white) ![WSGI Gunicorn](https://img.shields.io/badge/WSGI-Gunicorn-499848?logo=gunicorn&logoColor=white)  ![UI Bootstrap](https://img.shields.io/badge/UI-Bootstrap_3-563d7c?logo=bootstrap&logoColor=white)  ![Environment Conda](https://img.shields.io/badge/environment-conda-blue?logo=anaconda&logoColor=white)  ![License MIT](https://img.shields.io/badge/license-MIT-green)  ![Status](https://img.shields.io/badge/status-Deployed-brightgreen)  


This is a guided Django project built while following *Python Crash Course* by Eric Matthes.

It’s a **web application** that lets users:

- ✅ Register and log in.  
- ✅ Create topics to organize their learning.  
- ✅ Add, edit, and view entries under each topic.  
- ✅ Manage their personal learning journal in the cloud.  


Tthis project was also deployed to **Heroku** with a  **PostgreSQL database** so it’s accessible online.  

🔗 **Live Demo:** [Learning Log on Heroku](https://learning-log-jka-4767507ea9b2.herokuapp.com/)  



---


## Features

- **User Authentication**: register, log in, and log out securely.

- **Topics**: create new learning topics and manage them.

- **Entries**: add journal-style entries under each topic.

- **Responsive UI**: styled with Bootstrap for a clean, simple layout.
- **Deployment**: Runs on Heroku with WhiteNoise for static files.  
- **Databases**:  
  - **SQLite** → used for **local development**
  - **PostgreSQL** → used for production on **Heroku**  
---



## Tech stack

- **Backend**: Django (Python 3.11)  
- **Database**: SQLite (development) → PostgreSQL (production on Heroku)  
- **Frontend**: HTML, Bootstrap 3 (via django-bootstrap3)  
- **Deployment**: Heroku (with Procfile, Whitenoise, and dj-database-url)  




## Project structure


- **`learning_log/`** – Project configuration (settings, URLs, WSGI/ASGI)  
  - `settings.py` – Settings: debug, static, databases (SQLite/Heroku Postgres)  
  - `urls.py` – Root URL routing  
  - `wsgi.py` – WSGI entry point for deployment  
  - `asgi.py` – ASGI entry point (not used here, but standard Django)  

- **`learning_logs/`** – Core app: handles learning topics & entries  
  - `models.py` – Database models: Topic, Entry  
  - `views.py` – App logic: CRUD for topics/entries  
  - `forms.py` – Django forms for new topics/entries  
  - `urls.py` – Routes for the app  
  - `templates/` – Templates for topics, entries, base layout  
  - `migrations/` – Database migrations for this app  

- **`users/`** – Authentication app: login & register  
  - `views.py` – Handles register, login, logout  
  - `urls.py` – Routes for user authentication  
  - `templates/users/` – Templates: `login.html`, `register.html`  
  - `migrations/` – User-related migrations  

- **`manage.py`** – Django’s CLI utility  
- **`requirements.txt`** – Project dependencies  
- **`Procfile`** – Declares the process to run on Heroku  
- **`static/`** – (Optional) static assets (CSS/JS/images, if added)  




## Glossary of Key Files  

###   Project-level (`learning_log/`)  

- **`settings.py`** → Main configuration file. Defines database, apps, middleware, static files, and security settings.  
- **`urls.py`** → Routes requests to the correct app. Example: `/users/` goes to the **users app**, `/` goes to **learning_logs**.  
- **`wsgi.py`** → Entry point for running Django on servers like **Heroku**.  
- **`asgi.py`** → Async entry point (not actively used here, but included by default in Django projects).  




###  Core App (`learning_logs/`)  

- **`models.py`** → Defines the database schema. Contains two models:  
  - **`Topic`** → A subject the user is learning.  
  - **`Entry`** → Detailed notes linked to a specific Topic.  

- **`views.py`** → Handles request/response logic. Implements CRUD (**Create, Read, Update, Delete**) for topics and entries.  

- **`forms.py`** → Defines Django forms for creating and editing topics and entries. Uses Django’s built-in form handling system.  

- **`urls.py`** → App-specific routes (e.g., `/topics/`, `/topics/1/`). Maps user requests to the correct view functions.  

- **`templates/`** → HTML templates that render the app’s UI. Uses Django Template Language (**DTL**) to dynamically display topics, entries, and user data.  

- **`migrations/`** → Auto-generated files that track database schema changes (e.g., when adding a new model field). These ensure database consistency when models evolve.  



###  Authentication App (`users/`)  

- **`views.py`** → Contains the logic for:  
  - registering new users.  
  - logging in.  
  - logging out.  

- **`urls.py`** → App-specific routes for authentication, such as:  
  - `/users/login/` → Login page.  
  - `/users/register/` → Registration page.  

- **`templates/users/`** → HTML templates for login and registration forms:  
  - `login.html` → User login form.  
  - `register.html` → New user signup form.  

- **`migrations/`** → Tracks any database changes related to the `users` app (though most authentication data comes from Django’s built-in `auth` app).  



###  Other Files  

- **`manage.py`** → Django’s command-line utility. Used to run key commands such as:  
  - `runserver` → Start the development server.  
  - `migrate` → Apply database migrations.  
  - `createsuperuser` → Create an admin user.  

- **`requirements.txt`** → Lists all project dependencies so they can be installed consistently.  
  - Includes: `Django`, `psycopg2` (PostgreSQL adapter), `dj-database-url`, `whitenoise`, etc...  

- **`Procfile`** → Required by Heroku. Defines how to run the app in production:  
  ```bash
  web: gunicorn learning_log.wsgi
  ```
- **`static/`** → (Optional) holds static files like CSS/JS if you add them.



## Setup Instructions

### 1️⃣ Clone the repository
```bash
git clone https://github.com/JKA098/Learning-log-with-django.git
cd Learning-log-with-django
```

### 2️⃣ Create a Conda environment & install dependencies
```bash
# Create a new conda environment
conda create -n learning_log python=3.11

# Activate the environment
conda activate learning_log

# Install dependencies
pip install -r requirements.txt
```




### 3️⃣ Run locally with SQLite (development/optional)

You first need to configure `SQLite` as the fallback database in settings.py:
```bash
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

➡️Then visit: 
```bash
http://localhost:8000/
```

### 4️⃣ Deploy to Heroku with PostgreSQL (production)

#### 1. Provision PostgreSQL (essential-0 plan):

```bash
# First you need to create a Heroku account, 
# then login in the command line wiht:
# heroku login
heroku addons:create heroku-postgresql:essential-0

```


#### 2.Push code to Heroku:
```bash
git push heroku master

```


#### 3.Run migrations on PostgreSQL:
```bash
heroku run python manage.py migrate

```


#### 4.Create an admin user (superuser):
```bash
heroku run python manage.py createsuperuser

```


Then visit: 
```bash

https://learning-log-jka-4767507ea9b2.herokuapp.com/

```



##  What I Learned


- **Django apps structure** → How Django apps are structured *(project vs apps).* 
- **MVT Pattern** → How to implement *models, views, and templates (MVT pattern).*  
- **Authentication** → Using Django’s *auth system for login/register.*  
- **Static Files** → Serving static files with *WhiteNoise.*  
- **Deployment** → How to deploy a *Django app to Heroku with PostgreSQL.*  




### Screenshots for heroku deployment:

#### - Homepage
![Homepage](picture\heroku_dev\0_home_page.png)

#### - Topics Page
![Topics](picture\heroku_dev\1_topic_main_page.png)

#### - Registration page
![Registration page](picture\heroku_dev\2_registration_page.png)

#### - Login page
![Login page](picture\heroku_dev\3_1_login_page.png)

#### - Login page example
![Login page example](picture\heroku_dev\3_login_page.png)



### Screenshots for local deployment:

#### - Homepage
![Homepage](picture\local_dev\0_home_page.png)

#### - Topics Page
![Topics](picture\local_dev\1_topic_main_page.png)

### - Topic example
![Topic example](picture\local_dev\1_1_topic_example.png)

#### - Registration page
![Registration page](picture\local_dev\2_registration_page.png)

#### - Login page
![Login page](picture\local_dev\3_login_page.png)




##  Notes  

- *Locally*, the project runs on **SQLite** for simplicity.  
- *In production (Heroku)*, it uses **PostgreSQL (Essential-0 ).**  
- Static files are handled via **Whitenoise.**  
- **ALLOWED_HOSTS** is set for *all* for simplicity.  


## Acknowledgments

This project is based on the guided example from *Python Crash Course* (Eric Matthes) with modifications for deployment and database setup.  



