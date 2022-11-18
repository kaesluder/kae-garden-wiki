# Workflow for creating heroku app


`hobby-dev` might be outdated with recent service changes. 

```shell
source venv/bin/activate
pip install gunicorn
pip freeze > requirements.txt
touch Procfile
heroku login
heroku create kaes-task-list-api
git remote -v
git status
git push heroku master:main
heroku addons:create heroku-postgresql:hobby-dev
heroku run flask db upgrade
 ```