# Quick Start

This guide will help you install Harp. You’ll create and serve a simple project in `development` mode, where preprocessing occurs automatically, and then in `production` mode, where the preprocessed output is cached for better performance.

1. ## Install the Harp Web Server

  <div class="videoWrapper"><iframe width="853" height="480" src="//www.youtube.com/embed/SEA0G9kpVJM?rel=0" frameborder="0" allowfullscreen></iframe></div>

  First, install [Node.js](https://nodejs.org/download/). Harp uses Node.js, but you don’t need to know about Node.js or even JavaScript to use Harp. Once it’s finished installing, you can install Harp using the mighty npm: Node.js’ package manager. You’ll use the command prompt to do this.

  ### On OS X and Linux

  Access the command prompt using the Terminal application. On OS X, it’s located in Applications → Utilities → Terminal. On Ubuntu, find it in Applications → Terminal. Then, run the following command:

  ```bash
  sudo npm install -g harp
  ```

  ### On Windows

  If you are using Windows, NodeJS will have come with the Node.js Command Prompt application. Now, to install Harp via npm, type in:

  ```bash
  npm install -g harp
  ```

2. ## Create an Application

  Harp will serve something as simple as an `index.html`. But, because Harp has built-in preprocessing, you can create HTML with a templating language just as easily. Create an `index.jade` file instead. To do this using the command line, run the following:

  ```sh
  mkdir hello-world
  cd hello-world
  echo h1 Hello World >> index.jade
  ```

  This will make a `hello-world/` directory for your Harp app. Then, inside that directory, an `index.jade` file is created that will be served as `<h1>Hello world</h1>`.

3. ## Start the web server

  Fire up the Harp web server on the default port, `9000`.

  ```sh
  harp server --port 9000
  ```

  Visiting [localhost:9000](http://localhost:9000) will now show the following:

  ![Harp “Hello world” in the browser](/docs/images/hello-world.png)

4. ## Compile the project

  Optionally to running as a web server you can compile to be run with a webserver of your choice. Harp makes for a great static site generator.

  ```sh
  harp compile
  ```

5. ## Putting Harp in Production

  This is all you need to put a Harp application into production. In production mode, Harp will cache the preprocessed output—in this case, from `index.jade`—to serve the files as quickly as possible. Always use this `production` flag when putting Harp in production:

  ```sh
  NODE_ENV=production sudo harp server --port 80
  ```

  You don’t need to manually run Harp in production to get your project online, however. The easiest way to get started is to use the [Harp Platform](https://www.harp.io/), which lets you create and collaborate on Harp apps right in your Dropbox.

  You can also run Harp in production on [Heroku](https://harp.sh/docs/deployment/heroku), deploy Harp to [GitHub Pages](https://harp.sh/docs/deployment/github-pages), compile your app for Apache Cordova/PhoneGap, and more.

## What’s Next

This is just a taste of what Harp can do for you. For example, the default Harp application also includes a `.less` file that is automatically served as `.css`. Being able to change the CSS just by editing the LESS file—no configuration necessary—makes the default app a good starting point for your own project; [read more about initializing the default Harp app.](/docs/environment/init)