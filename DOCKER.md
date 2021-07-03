## Docker
- [Docker WSL](https://github.com/ArisOther/deploy/blob/main/DOCKER-WSL.md)
- [Docker - Programmer Jaman Now](https://github.com/ArisOther/deploy/blob/main/DOCKER-PJN.md)
- [Docker-Pawamoy - Django,gunicorn,psql,redis](https://github.com/ArisOther/Docker-pawamoy)

##
- sample 1

  ```yml
  version: '3'

  services:

    djangoapp:
      build: .
      volumes:
      - .:/opt/services/djangoapp/src
      - static_volume:/opt/services/djangoapp/static  # <-- bind the static volume
      - media_volume:/opt/services/djangoapp/media  # <-- bind the media volume
      networks:
      - nginx_network
      - database1_network
      depends_on:
      - database1

    nginx:
      image: nginx:1.13
      ports:
      - 8000:80
      volumes:
      - ./config/nginx/conf.d:/etc/nginx/conf.d
      - static_volume:/opt/services/djangoapp/static  # <-- bind the static volume
      - media_volume:/opt/services/djangoapp/media  # <-- bind the media volume
      depends_on:
      - djangoapp
      networks:
      - nginx_network

    database1:
      image: postgres:10
      env_file:
      - config/db/database1_env
      networks:
      - database1_network
      volumes:
      - database1_volume:/var/lib/postgresql/data

  networks:
    nginx_network:
      driver: bridge
    database1_network:
      driver: bridge

  volumes:
    database1_volume:
    static_volume:  # <-- declare the static volume
    media_volume:  # <-- declare the media volume
  ```
- sample 2
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
