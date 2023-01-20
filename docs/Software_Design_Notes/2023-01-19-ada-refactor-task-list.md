# Modding Task List to Be Demo Friendly

Notes on modding the [task list](https://github.com/kaesluder/task-list-api) project to make it more friendly to download and use as a portfolio piece. My goal here is to make downloading and installing task list a bit easier for people who don't really want to go through postresql setup or downloading a separate repo for the front end. Some of the steps include:

1. Setting the database to use sqlite.
2. Configuring flask to hosting it's own web front-end.
3. Creating install and demo scripts.
4. Rewriting documentation.

The target of this refactor is to allow for people to download and run the project needing only python3.

**Warn:** These mods could break things. Do this in a fork or separate branch, and run `pytest` frequently.

## Changing the Database to sqlite

Task List was built to use [postgresql](https://www.postgresql.org/). Why [sqlite](https://www.sqlite.org/index.html)? Sqlite is a stand-alone database that has the following features:

1. zero config
2. no open ports for people who use firewalls or other port-based security
3. compatible with a wide spectrum of SQL and programming languages
4. no need to worry about database user permissions

Sqlite may not scale well to full web deployment, and the ability to switch back and forth between sqlite and postgresql is very dependent on which SQL features your app uses.

The final product for the [task list backend](https://github.com/kaesluder/task-list-api) uses [python dotenv](https://pypi.org/project/python-dotenv/) to read environment variables from a file in the root directory of the project named `.env`. Switching over is simply a matter of changing the environment variables in the `.env` file.

```sh
# .env
SQLALCHEMY_DATABASE_URI=sqlite:////tmp/test.sqlite
SQLALCHEMY_TEST_DATABASE_URI=sqlite:////tmp/test2.sqlite
```

This config will create sqlite files in the /tmp folder of your operating system. These files are purged on a regular basis.

- [SQLAlchemy connection URI documentation](https://docs.sqlalchemy.org/en/13/core/engines.html#sqlite)

## Giving The API a Front Page

The next step is to copy the [react front-end](https://github.com/kaesluder/task-list-front-end) into our flask app, and tell the flask app to serve the front end at `http://localhost:5000/`. We also need to tell flask to serve _all_ of the assets needed by our front page.

In the _front end_ development folder edit `package.json` to set the `homepage` to the URL that the page is served from.

```JavaScript
  \\package.json
  "homepage": ".",
```

Build an compiled and optimized version with `yarn build` then copy the everything in your build folder into `task-list-api/app/static`.
`static` is the default flask folder for serving static files. Your app folder should look something like this:

```
app
├── __init__.py
├── goal_routes.py
├── models
│   ├── __init__.py
│   ├── __pycache__
│   ├── goal.py
│   └── task.py
├── route_helpers.py
├── slackbot.py
├── static
│   ├── asset-manifest.json
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   ├── robots.txt
│   └── static
├── task_routes.py
└── util_routes.py
```

After that we need to tell flask to serve static assets at the _root_ of our web site. Open `task-list-api/app/__init__.py` and add `static_url_path=""` to the `Flask()` call in `create_app()`.

```python
# task-list-api/app/__init__.py
def create_app(test_config=None):
    app = Flask(__name__, static_url_path="")
```

The next configuration step sets `task-list-api/app/static/index.html` as the default web page for the server. Further down in `create_app()` add the following.

```python
# task-list-api/app/__init__.py

    @app.route("/")
    def root_index():
        return send_from_directory("static", "index.html")
```

"If a user requests the url `/`, send `index.html` from the `static` folder."

**Warn**: Flask is picky about file paths. Make sure that `task-list-api/app/static/index.html` exists.

### CORS

If you have not already done so, install and enable [flask-cors](https://flask-cors.readthedocs.io/en/latest/).

```python
# task-list-api/app/__init__.py

from flask_cors import CORS
...
def create_app(test_config=None):
    app = Flask(__name__, static_url_path="")
    CORS(app)

```

After all this, start up `flask serve` and you should find your front-end at http://localhost:5000/
