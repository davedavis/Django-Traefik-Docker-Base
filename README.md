# What is this?
Cookiecutter Django is great. But it's a bit heavy, complex and error-prone when you just
want to get a project started quickly. I just wanted a production ready django project with
the following requirements: 

1) A basic installation of the most recent version of Django
2) Runs in docker
3) Traefik instead of NginX to handle letsencrypt easier
4) Whitenoise for static files
5) Allauth with Google signin/signup installed
6) Works with cloudflare proxied DNS
7) Has a nice admin

This is a django base project that lets me get moving on a new side project quickly. 
Think of it as a much less complicated version of cookiecutter django.

**This project takes advantage of Django's weird convention that a project contains 
apps and that the actual functionality should be set up in an app** This project is 
just the project part of that equation. To get up and running quickly:

 - Simply clone this project
 - Set your domain/env variables in the .env file.
 - Change your email address in the traefik.prod.toml file
 - Start the Django tutorial from the [app creation section](https://docs.djangoproject.com/en/4.1/intro/tutorial01/#creating-the-polls-app)
   . e.g, python manage.py startapp polls



# Deployment
Important: If you're using CloudFlare, ensure cloudflare full SSL is set.

1) docker-compose -f docker-compose.prod.yml down -v
2) sudo rm -r traefik-public-certificates/
3) git pull
4) docker-compose -f docker-compose.prod.yml up -d --build
5) docker-compose -f docker-compose.prod.yml logs -f
6) docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
7) docker-compose -f docker-compose.prod.yml exec web python manage.py createsuperuser
8) docker-compose -f docker-compose.prod.yml logs -f

# Running Locally

1) docker-compose down -v 
2) docker compose up -d --build
3) docker-compose -f docker-compose.yml logs -f


# Notes
    Make sure you edit your /etc/hosts file to point your DEV_DOMAIN in the env file to 0.0.0.0
    Make sure you set your cloudflare SSL settings to "full", not flexible.
    I run other containers locally, so extracted DEV_PORT so I wouldn't get confused. 

#### Remember: Do **NOT** add your .env file to source control. I did it for your convenience only. 
