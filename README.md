# Appointment Reminders (Django)

[![Build Status](https://travis-ci.org/TwilioDevEd/appointment-reminders-django.svg?branch=master)](https://travis-ci.org/TwilioDevEd/appointment-reminders-django)

Use Twilio to create automatic appointment reminders for your business's clients.

[Read the full tutorial here](https://www.twilio.com/docs/tutorials/walkthrough/appointment-reminders/python/django)!

## Quickstart

### Local development

This project is built using the [Django](https://www.djangoproject.com/) web framework. It runs on Python 2.7+ and Python 3.4+.

To run the app locally, first clone this repository and `cd` into its directory. Then:

1. Create a new virtual environment:
    - If using vanilla [virtualenv](https://virtualenv.pypa.io/en/latest/), run `virtualenv venv` and then `source venv/bin/activate`
    - If using [virtualenvwrapper](https://virtualenvwrapper.readthedocs.org/en/latest/), run `mkvirtualenv appointments`
1. Install the requirements with `pip install -r requirements.txt`
1. Start a local PostgreSQL database and create a database called `appointment_reminders`
    - If on a Mac, I recommend [Postgres.app](http://postgresapp.com/). After install, open psql and run `CREATE DATABASE appointment_reminders;`
    - If Postgres is already installed locally, you can just run `createdb appointment_reminders` from a terminal
1. Run the migrations with `python manage.py migrate`
1. Optionally create a superuser so you can access the Django admin: `python manage.py createsuperuser`
1. Copy the `.env_example` file to `.env`, and edit it to include your Twilio API credentials (found at https://www.twilio.com/user/account/voice)
1. Run `source .env` to apply the environment variables (or even better, use [autoenv](https://github.com/kennethreitz/autoenv))
1. Start the development server: `python manage.py runserver`

This project uses [Celery](http://docs.celeryproject.org/en/latest/index.html) to asynchronously send SMS reminders to users. To start the Celery process:

1. This project uses [Redis](http://redis.io/) as its task queue. Install and start Redis
1. Start a new terminal session and activate your virtual environment
1. Source the `.env` file if you're not using [autoenv](https://github.com/kennethreitz/autoenv)
1. Start the Celery worker with the command: `celery -A appointments.settings worker -l info`

You can then visit the application at [http://localhost:8000/](http://localhost:8000/).

## Run the tests

You can run the tests locally through [coverage](http://coverage.readthedocs.org/en/coverage-3.7.1/#):

```
$ coverage run manage.py test --settings=appointments.settings.test
```

You can then view the results with `coverage report` or build an HTML report with `coverage html`.
