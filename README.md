# flask-swagger-ui

Simple Flask blueprint for adding [Swagger UI](https://github.com/swagger-api/swagger-ui) to your flask application.

Included Swagger UI version: 4.11.1.

## Modification required if using an entry point like ```/api/v1```
Problem: When added an entry point, swagger.json absolute path to be given in the search bar of swagger page. Or you are required to give double entry point like ```/api/v1/api/v1```.

Solution: [checkout here](https://github.com/gaurav-basesolve/flask-swagger-ui/blob/2a3049e86a65a90f9beb6efe7c5814d06a21fdab/flask_swagger_ui/flask_swagger_ui.py#L31)

## Installation

When not using entry point: `pip install flask-swagger-ui`

With entry point: `pip install git+https://github.com/gaurav-basesolve/flask-swagger-ui.git`

## Usage

Example application:

```python
from flask import Flask
from flask_swagger_ui import get_swaggerui_blueprint

app = Flask(__name__)


SWAGGER_URL = '/docs'  # URL for exposing Swagger UI (without trailing '/')
API_URL = '/api/v1/swagger.json'  # Our API url (can of course be a local resource)

# Call factory function to create our blueprint
swaggerui_blueprint = get_swaggerui_blueprint(
    SWAGGER_URL,  # Swagger UI static files will be mapped to '{SWAGGER_URL}/dist/'
    API_URL,
    config={  # Swagger UI config overrides
        'app_name': "Test application"
    },
    # oauth_config={  # OAuth config. See https://github.com/swagger-api/swagger-ui#oauth2-configuration .
    #    'clientId': "your-client-id",
    #    'clientSecret': "your-client-secret-if-required",
    #    'realm': "your-realms",
    #    'appName': "your-app-name",
    #    'scopeSeparator': " ",
    #    'additionalQueryStringParams': {'test': "hello"}
    # }
)

app.register_blueprint(swaggerui_blueprint)

app.run()

# Now point your browser to localhost:5000/api/docs/

```

## Configuration

The blueprint supports overloading all Swagger UI configuration options that can be JSON serialized.
See https://github.com/swagger-api/swagger-ui/blob/master/docs/usage/configuration.md#parameters for options.

Plugins and function parameters are not supported at this time.

OAuth2 parameters can be found at https://github.com/swagger-api/swagger-ui#oauth2-configuration .
