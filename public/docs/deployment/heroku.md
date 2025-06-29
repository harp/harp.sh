# Deploying on Heroku

Heroku is a developer-focused platform for hosting applications.

If you’re familiar with using git in the command line, you’ll have no trouble deploying your Harp app to Heroku.

## Create a Heroku account

If you haven’t already, create a [Heroku account](https://signup.heroku.com/signup/dc) and install their [toolbelt](https://toolbelt.heroku.com/). Then, using the Terminal, login with the username and password you chose:

```sh
heroku login
```

## Create or use an existing application

Now you’re ready to being modifying your Harp app to prepare it for Heroku. If you don’t have an existing app, or would like to try out deployment with the default app, you may [use `harp init` to initialize a new application](/docs/environment/init).

Otherwise, create a directory with an index file. You can do this with the terminal, too:

  ```sh
  mkdir my-harp-app
  cd my-harp-app
  echo "hello world" > index.html
  ```

## Add `package.json` and `Procfile`

  There are two files you’ll need to add to the root of your Harp application (not inside the `public` directory). The first is `package.json`:

  ```json
   {
     "name": "My-Harp-App",
     "version": "1.0.0",
     "description": "A Harp App on Heroku",
     "dependencies": {
       "harp": "*"
     }
   }
   ```

  If you already have a `package.json`, the easiest way to add harp to the dependency list is by running:

  ```sh
  npm install harp --save
  ```

  Next, create `Procfile`, which should contain the following:

  ```
  web: harp server --port $PORT
  ```

## Initialize your app as a Git repo

  Using the terminal, initialize your Harp app as a Git repository (if it isn’t one already). Then, add and commit the changes:

  ```sh
  git init
  git add .
  git commit -am "First Harp + Heroku commit"
  ```

## Deploy to Heroku

   You’re ready to deploy to Heroku. Create the Harp app as a Heroku app, use `git` to push the app to Heroku, and then open the site in your browser:

   ```sh
   heroku create my-harp-app
   git push heroku master
   heroku open
   ```

   In this example, the application will be named `my-harp-app`, and should be immediately available at `my-harp-app.herokuapp.com`.

##### What’s Next?

Your Harp app has been successfully deployed to Heroku. Now, you’d probably like to customize it. Read the [five simple rules](https://harp.sh/docs/development/rules) for templating a Harp application to get started quickly.

If you’d like to use a custom domain with Heroku, follow the instructions in the [Heroku Dev Center](https://devcenter.heroku.com/articles/custom-domains).
