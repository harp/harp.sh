# Azure

Microsoft Azure is an open and flexible cloud platform that enables you to quickly build, deploy and manage applications across a global network of Microsoft-managed data centres.

If you’re familiar with using git in the command line, you’ll have no trouble deploying your Harp app to Azure.

## Azure Cross-Platform Command Line

First, download the [Azure Cross-Platform Command Line for Node](https://github.com/Azure/azure-sdk-for-node).
We will use this tool to help create the Azure site from the command line.

```sh
npm install -g azure-cli
```

An more in-depth blog post about the tool can he found [here](http://www.hanselman.com/blog/WindowsAzureNoKidding.aspx)

1. ## Create or use an existing application

  If you need a new application, create a directory with an index file. You can do this with the terminal, too:

  ```sh
  harp init my-harp-app
  cd my-harp-app
  ```

2. ## Initialize your app as a Git repo

  Next, you’ll initialize your Harp app as a Git repository (if it isn’t one already.) Then, add and commit the changes:

  ```sh
  git init
  git add .
  git commit -am "hello world"
  ```

3. ## Add `package.json` and `server.js`

  There are two files you’ll need to add to the root of your Harp application (not inside the `public` directory). The first is `package.json`:

  ```json
  {
   "name": "MyHarpApp",
   "version": "1.0.0",
   "description": "A Harp App on Azure",
   "dependencies": {
     "harp": "0.19.0"
   },
   "engines": {
     "node": "4.1.x",
     "npm": "3.5.1"
   }
  }
  ```

  Then, use Node Package Manager to install the dependencies:

  ```
  npm install
  ```

  Next, create `server.js`, which should contain the following:

  ```js
  require('harp').server(__dirname, { port: process.env.PORT || 5000 })
  ```

4. ## Deploy your Harp app to Azure

  You’re ready to deploy to Azure. Create the Harp app as an Azure project, where `my-harp-app` is the name of the subdomain you want:

  ```sh
  azure site create --location "West US" my-harp-app --git
  ```

  This will add a new `azure` remote to your git repository. The `azure` remote is how the site will be deployed. To deploy to azure is as simple as pushing to master.

  ```
  git push azure master
  ```
5. ### Set environment to production

  To get the best performance, you’ll need to set Harp’s production properly.

  ```sh
  azure config set NODE_ENV production
  ```

  At this point your site should be running on Azure at `http://my-harp-app.azurewebsites.net`, but with the subdomain you specifed instead of `my-harp-app`.

## What’s next?

Your Harp app has been successfully deployed to Azure. Now, you’d probably like to customize it. Read the [five simple rules](https://harp.sh/docs/development/rules) for templating a Harp application to get started quickly.

If you’d like to use a custom domain with Azure, follow the instructions in the [Microsoft Azure Documentation](http://azure.microsoft.com/en-us/documentation/articles/cloud-services-custom-domain-name/).
