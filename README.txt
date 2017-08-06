cd /users/raynovarina/sites/AtomProjects/harp/greensock-getting-started/

per: https://greensock.com/jump-start-js
     https://greensock.com/get-started-js#intro

Cloned from my repos:

$ git clone https://github.com/RayNovarina/harp-heroku-mdn-canvas-tutorial.git greensock-getting-started
$ cd greensock-getting-started/

Start harp server:
$ harp server -p 9007

Access via localhost:9007
============================

Modify package.json and Procfile files for Heroku deploy:
  package.json:

    {
      "name": "greensock-tutorial",
      "version": "0.0.1",
      "description": "Harp server App: javascript/greensock-tutorial",
      "dependencies": {
          "harp": "*"
      }
    }

  Procfile:

    web: harp server --port $PORT

At github account, create new repository: harp-heroku-greensock-getting-started and then
locally.
  $ git init
  $ git remote add origin https://github.com/RayNovarina/harp-heroku-greensock-getting-started.git

Create Heroku app:
  $ heroku create harp-greensock-getting-started-94037

$ git remote -v
  heroku  https://git.heroku.com/harp-greensock-getting-started-9403.git (fetch)
  heroku  https://git.heroku.com/harp-greensock-getting-started-9403.git (push)
  origin  https://github.com/RayNovarina/harp-heroku-greensock-getting-started.git (fetch)
  origin  https://github.com/RayNovarina/harp-heroku-greensock-getting-started.git (push)

Deploy changes to github and heroku:
  $ git add .
  $ git commit -am "First Harp + Heroku commit"
  $ git push origin master
  $ git push heroku master

View on Heroku:

  https://harp-greensock-getting-started-9403.herokuapp.com shows:

  Welcome to harp/greensock-getting-started.
  Deployed locally at http://localhost:9007/
  Deployed on Heroku at https://harp-greensock-getting-started-94037.herokuapp.com/

=========================================================
