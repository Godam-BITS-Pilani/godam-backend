# Godam Backend

This repository contains the backend for the Godam dashboard. It uses Django Rest Framework
to serve a REST API for the React client. It uses Postgres for the database and Celery running
on a Redis instance for state management and task queues. 

### Features
* Auth: Provides user authentication, management using Knox Tokens. User's are able to verify their emails and phone numbers with OTP emails and SMS sent to them. 
* Content: Provides a CMS through the admin dashboard to serve blog posts and other content types to the dashboard. This also includes data collection and analysis.

## API Documentation:
The documentation is currently available as a Postman collection posted on
the Organization's Notion page.

## API Build instructions: 

The dependencies are managed by Pipenv. To activate the 
virtual environment do the following: 

1. `pip install pipenv`
2. `pipenv install --dev`
3. `pipenv shell`

At this point you will need the `.env` file to get the app to run. To get this
file please contact Param at paramkapur2002@gmail.com for further instructions.

Now you will need other pre-requisites:
1. `postgresSQL`
    * Please set it up on your machine and create a local database to connect to. Put
    this localhost URL in the `DATABASE_URL` environment variable.
2. `redis`
    * Install the latest version and have a server running on port 6043. 
    
Finally, you can run the app with:
`python manage.py runserver`

Which will start a server at `localhost:8000`.



## Notes
#### User Authentication Classes on an APIView
```python
from rest_framework.views import APIView
from rest_framework.permissions import IsAuthenticated
from knox.auth import TokenAuthentication

class SomeView(APIView):
    # ...
    permission_classes =  (IsAuthenticated,)
    authentication_classes = (TokenAuthentication,)
    # ...
```
