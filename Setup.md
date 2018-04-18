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


#### Roll out
```bash
workon lightweight_django_chapter4
docker rm `docker ps -a|grep lightweightdjangochapter4_db|cut -d' ' -f1` 
rm -fr ./database
mkdir database
createdb -E UTF-8 scrum -U postgres
#update DATABASE in settings.py
d-c up -d --build
http://127.0.0.1:8000/api/
```

#### Clean up
```bash
d-c down
```
#### Diagnose
```bash
docker exec -it `docker ps|grep lightweightdjangochapter4_db|cut -d' ' -f1` bash
psql -U postgres
\l
\dt
\q
```
