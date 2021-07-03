## Docker
- [Docker WSL](https://github.com/ArisOther/deploy/blob/main/DOCKER-WSL.md)
- [Docker - Programmer Jaman Now](https://github.com/ArisOther/deploy/blob/main/DOCKER-PJN.md)
- [Docker-Pawamoy - Django,gunicorn,psql,redis](https://github.com/ArisOther/Docker-pawamoy)

##
- sample 1
  ```yml
  version: "3.2"
  services:
    app:
      restart: always
      build:
        context: .
        dockerfile: Dockerfile.prodtest
        args:
          requirements: requirements/production.txt
      #command: bash -c "python manage.py makemigrations && python manage.py migrate && gunicorn --config gunicorn.conf --log-config loggigng.conf -e DJANGO_SETTINGS_MODULE=site.settings.production_test -W 4 -b 0.0.0.0:8000 site.wsgi"
      container_name: dj01
      environment:
        - DJANGO_SETTINGS_MODULE=site.settings.production_test
        - PYTHONDONTWRITEBYTECODE=1
      volumes:
        - ./:/app
        - /static:/static
        - /media:/media
      networks:
        - main
      depends_on:
        - db
  ```
