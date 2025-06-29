# Deploying to Nodejitsu

Heroku is a developer-focused platform for hosting Node-based applications.

If you’re familiar with using git in the command line, you’ll have no trouble deploying your Harp app to Heroku.

1. ## Create a Nodejitsu account

  If you haven’t already, create a [Nodejitsu account](https://www.nodejitsu.com/signup/). Install their command line tool using:

  ```bash
  sudo npm install -g jitsu
  ```

  If you are using Windows, you can leave off `sudo`.

	Next, you’ll login to `jitsu` so you can deploy to Nodejitsu. You’ll have received an email from Nodejitsu to confirm your account. Included is a line you can copy and paste into the terminal that will look something like:

  ```bash
  jitsu users confirm yourusername a1234567-89bc-0de1-d23e-45fgh67890ij
  ```

  You should receive a message asking if you’d like to log in. Reply `yes`, and enter your Nodejitsu password.

  Now, you’re ready to prepare your Harp app for Nodejitsu. If you don’t have an existing app, or would like to try out Nodejitsu with Harp’s default app, you may [use `harp init` to initialize a new application](/docs/environment/init).

<!-- this is as far as I got, the rest is from the Herkou guide as a template -->

2. ## Add `package.json`, `server.js` and a `Procfile`

  There are three files you’ll need to add to the root of your Harp application (If you are running your app in “framework-style” and have an explicit `public/` directory, these files still need to in the root, above this directory).

  The first file necessary is the `package.json`:

  ```json
   {
     "name": "My Harp App",
     "version": "1.0.0",
     "description": "A Harp App on Nodejitsu",
     "dependencies": {
       "harp": "*"
     },
     "engines": {
       "node": "0.10.x",
       "npm": "1.2.x"
     }
   }
   ```

   Then, use npm to install the dependencies:

   ```
   npm install
   ```

   Next, create `server.js`, which will start Harp. It should contain the following:

   ```js
  require('harp').server(__dirname, { port: process.env.PORT || 5000 })
  ```

   Finally, add a `Procfile` in the root as well. The `Procfile` is a text file that executes the `server.js` file you just created. It only needs to be this one line:

   ```
    web: node server.js
    ```

3. ## Initialize your app as a Git repo

   Using the terminal, initialize your Harp app as a Git repository (if it isn’t one already.) Then, add and commit the changes:

  ```sh
  git init
  git add .
  git commit -m "First Harp + Heroku commit"
  ```

4. ## Deploy to Heroku

   You’re ready to deploy to Heroku. Create the Harp app as a Heroku app, and then use `git` to push the app to Heroku.

  ```sh
  heroku create
  git push heroku master
  ```

5. ## Rename your application

   Heroku generates a name for your application, something like `lit-chamber-9232`. Chances are you don’t want this to be your app’s name. In the following example, the application will be renamed to `my-harp-app`, and should be immediately available at `my-harp-app.herokuapp.com`.

  ```sh
  heroku apps:rename my-harp-app
  ```

##### What’s Next?

Your Harp app has been successfully deployed to Heroku. Now, you’d probably like to customize it. Read the [five simple rules](https://harp.sh/docs/development/rules) for templating a Harp application to get started quickly.

If you’d like to use a custom domain with Heroku, follow the instructions in the [Heroku Dev Center](https://devcenter.heroku.com/articles/custom-domains).