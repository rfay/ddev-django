# Demonstration of DDEV config for Django 4

This is a simple configuration using existing techniques to run Django 4 (with gunicorn) in DDEV. It's intended as a proof-of-concept for providing a webserver-type like `nginx-django` or `nginx-django4`

The "demo" app here is just the [app from the django4 tutorial](https://docs.djangoproject.com/en/4.0/intro/tutorial01/)


## Instructions for demonstration

* `ddev start`
* `ddev snapshot restore basic-running`
* `ddev launch /admin/` or `ddev launch /polls` (login is admin/admin)


## Questions and directions

1. DB credentials are wired into settings.py. Probably we'll want to do something like we do for settings.ddev.php for drupal.
2. Web serving is done with gunicorn. Probably we should have project types like django4 and webserver-types of nginx-gunicorn. 

## Things to inspect and that need guidance

1. [Special DDEV config](.ddev/config.django.yaml) is separated out into config.django.yaml for this project. 
1. [Nginx config](.ddev/nginx_full/nginx-site.conf) - input requested. This would move to a default nginx-gunicorn config.
2. [Gunicorn config](demo/config/gunicorn/dev.py) - Input requested.
3. [Dev settings](demo/demo/settings.py) are set up with DEBUG=true and static file handling by default (without gathering).

## Paths forward

1. Convert the gunicorn configuration into a webserver-type which determines how and what we start up in supervisord.
2. Move the gunicorn configuration out of the project?
3. Project type of django or django4 could determine settings file behavior and possibly add handling of static files.