#### Original repository
    https://github.com/lightweightdjango/examples

### First time pre-steps
```text
(*) -> run first time only
/etc/hosts -> 127.0.0.1	db
run profile -> runserver 0.0.0.0:8001
Admin credentials -> U:admin P:qwerty123
bash_profile -> alias d-c="docker-compose" alias d-r="docker-compose run web"
```

### Setup Environment (*)
```bash
rmvirtualenv django_tutorial_3_7
mkvirtualenv --python=/Library/Frameworks/Python.framework/Versions/3.6/bin/python3 django_tutorial_3_7
sudo easy_install pip
pip install --upgrade pip
pip install -r docker/requirements.txt
```

#### Roll out
```bash
workon django_tutorial_3_7
mkdir database
django-admin.py startproject scrum .
#update DATABASE in settings.py 
d-c up -d --build
docker ps
curl http://127.0.0.1:8000/
d-r python manage.py migrate
```


### Re-Start from scratch
```bash
d-c down
docker rmi `docker images|grep lightweightdjangochapter4|cut -d' ' -f1`
rm -fr database
```

### Final clean up
    remove -> /etc/hosts -> 127.0.0.1	db