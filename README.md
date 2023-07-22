# POS
A MariaDB/MySQL version of this [app](https://www.sourcecodester.com/python/15210/grocery-point-sales-pos-system-python-django-free-source-code.html)

## Installation
### 1. Creating a virtual environment
1. Install `virtualenv` to create an isolated environment for the project:
```bash
# install virtualenv
python3 -m pip install --user virtualenv
# check if installation was successful
python3 -m virtualenv --help
```
2. If `virtualenv` was successfully installed, you may now create an environment for the project:
```bash
# replace env_name with your name
# You mau use the conventional '.venv' as the name
virtualenv env_name
```
3. Activate the environment:

**Note:** You need to replace `env_name` below with the name you have chosen in #2

```bash
# In linux or macOS
source env_name/bin/activate

# Windows
.\env_name\Scripts\activate
```
#### 1.1 ℹ️ Alternative to `virtualenv`
If you cannot install `virtualenv`, you may use python's built-in `venv`:
```bash
# 1. Create a new virtual environment
python -m venv .venv

# 2. Activate the created virtualenv
# .venv is the name of the virtual env folder

# WSL/linux/macOS using zsh/bash
source .venv/bin/activate

# Windows
# cmd
.venv\Scripts\activate.bat
# Powershell
.venv\Scripts\Activate.ps1
```
---
### 2. Installing the required packages
1. In the root folder, install the required packages listed in `requirement.txt` using `pip`:
```bash
# macOS/linux
pip install -r requirements.txt

# Windows
python3 -m pip install -r requirements.txt
```
---
### 3. Preparing for the migration
1. Open `pos/settings.py` and look for `DATABASES` dictionary (see below, it's around line 80) to configure your connection string
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': '127.0.0.1',
        'PORT': '33306',
        'NAME': 'main_db', # replace with your db name
        'USER': 'root',
        'PASSWORD': 'pos123'
    }
}
```
In particular, you need to make sure that you have created a database in your MariaDB/MySQL server where Django will perform the migration. Also make sure that the other settings matches your connection configuration.

---
### 4. Migration
1. Perform the migration process as indicated by the instructions of the [original project](https://www.sourcecodester.com/python/15210/grocery-point-sales-pos-system-python-django-free-source-code.html)

**Note:** You must run the command in the root folder of the project, just like the other commands.

```bash
python3 manage.py migrate
```
---
### 5. Configure the user
1. The migration will not copy any data over your MariaDB/MySQL database, only the table schemas. Hence, we need to copy the superuser of the project so you could login to the app. 
2. To create the superuser account, run the following command in your MariaDB/MySQL server (using phpmyadmin, HeidiSQL, etc.):

**Note:** You must replace `main_db` below with the name of the database you have configured in your `DATABASE` configuration in `settings.py`

```SQL
-- replace main_db below
INSERT INTO main_db.auth_user (password, last_login, is_superuser, username, first_name, last_name, email, is_staff,
                               is_active, date_joined)
VALUES ('pbkdf2_sha256$600000$3jJmO0zgfArIXIdff9PWLb$F1Ld3TZSOIaUDV9GktzuRnN2/BdXnOBtps2kuEP6GGA=',
        '2023-07-21 16:43:04.536036', 1, 'admin', 'Administrator', '', 'admin@admin.com', 1, 1,
        '2022-03-04 01:27:51.000000');

```
---
### 6. Running the app
1. Assuming everything went well, you may now run the project:
```bash
python3 manage.py runserver
```
2. If there are no errors, navigate to the link shown in your terminal (it should look something like `http://127.0.0.1:8000`)
3. Use the following credentials to login:
```
Username: admin
Password: admin123
```
4. You may now start developing the project
