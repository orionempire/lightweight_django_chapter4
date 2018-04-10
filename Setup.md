#### Original repository
    https://github.com/lightweightdjango/examples

U:demo
P:demo1234

#### First time pre-steps
```text
(*) -> run first time only
/etc/hosts -> 127.0.0.1	db
add to pycharm run profile -> runserver 0.0.0.0:8001
bash_profile -> alias d-c="docker-compose" alias d-r="docker-compose run web"
```

#### Setup Environment (*)
```bash
rmvirtualenv lightweight_django_chapter4
deactivate
mkvirtualenv --python=/Library/Frameworks/Python.framework/Versions/3.6/bin/python3 lightweight_django_chapter4
sudo easy_install pip
pip install --upgrade pip
pip install -r docker/requirements.txt
```

```text
set project interpreter to lightweight_django_chapter4
```
d-c up -d --build

#### Roll out
```bash
workon django_tutorial_3_7
d-c stop db
docker rm `docker ps -a|grep lightweightdjangochapter4_db|cut -d' ' -f1` 
rm -fr ./database
mkdir database
d-c up -d db
docker exec -it `docker ps|grep lightweightdjangochapter4_db|cut -d' ' -f1` bash
createdb -E UTF-8 scrum -U postgres
exit
#update DATABASE in settings.py
cd scrum/
python manage.py makemigrations board
python manage.py migrate
python manage.py createsuperuser
```

http://127.0.0.1:8000/api/
### Database settings
```text
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
    
}
psql -U postgres
\l
\dt
\q
```
python -c "import sys; print(sys.path)"
