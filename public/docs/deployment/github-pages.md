# Deploying to GitHub Pages

GitHub Pages, also known as `gh-pages`, is GitHub’s free hosting service for public webpages. It is often used to host personal blogs and project websites.

If you’re familiar with using git in the command line, you’ll have no trouble deploying your Harp app to GitHub Pages.

## Example Usage

GitHub Pages can be used in two different ways:

* [User & Organization Pages](#user-pages)
* [Project Pages](#project-pages)

You can read more about the difference between the two kinds of pages in the [GitHub Pages documentation](https://help.github.com/articles/user-organization-and-project-pages).

<h2 id="user-pages">Deploying a GitHub User or Organization Page</h2>

These five steps will quickly walk you through deploying a Harp app to a personal or organization GitHub Page.

1. ### Create a New Repository

  Create a new repository called __your-github-user-name.github.io__, replacing “your-github-user-name” with your GitHub user or organization name. For example, if your username is octocat, you’d create a repository named octocat.github.io.

  ![The settings to use for your new repository on GitHub.](../images/github-pages-1.png)

  Tick “Initialize this repository with a README.” This will allow you to `clone` your new repository.

2. ### Clone the Repository

  In your terminal, `clone` the repository you just created:
    
  ```sh
  git clone https://github.com/your-github-user-name/your-github-user-name.github.io.git
  ```
    
3. ### Initialize a Harp app

  Your repository is ready, you just need a Harp app there. Initialize a new Harp app into `_harp`.

  ```sh
  harp init _harp
  ```

  If you have an existing project, you may also move it into your working directory, but make sure to name the folder with an underscore at the beginning; when you deploy to GitHub Pages, you don’t want your source files to be served.

4. ### Compile your Harp app

  Harp can compile your app to <abbr>HTML</abbr>, <abbr>CSS</abbr>, and JavaScript whenever you’d like. By default, `harp compile` creates a `www` directory. Because GitHub Pages are served from the root of the repository, however, you’ll want to compile your Harp app there instead.

  ```sh
  harp compile _harp ./
  ```

5. ### Deploy to GitHub Pages

  You’re ready to deploy your app! Add all the files, commit them, and push them to GitHub:

  ```sh
  git add -A
  git commit -a -m "First Harp + Pages commit"
  git push origin master
  ```

  Your app will be available at `your-github-name.github.io` within the next ten minutes.

##### What’s Next?

Your Harp app has been successfully deployed to GitHub Pages. Now, you’d probably like to customize it. Read the [five simple rules](https://harp.sh/docs/development/rules) for templating a Harp application to get started quickly.

If you’d like to use a custom domain with GitHub pages, follow the instructions in the [GitHub Pages documentation](https://help.github.com/articles/setting-up-a-custom-domain-with-pages).

***

<h2 id="project-pages">Deploying a Project Page</h2>

These five steps will quickly walk you through deploying a Harp app to a project’s GitHub Page.

1. ### Clone the Project

  ```sh
  git clone https://github.com/your-github-name/repository-name.git
  ```

2. ### Create a new, empty branch

  Next, you’ll need to create a new “orphan” branch in the app’s existing repository. This branch will contain your Harp app and the compiled HTML, CSS & JavaScript that will be served by GitHub Pages.

  ```sh
  cd repository
  git checkout --orphan gh-pages
  ```

  Now, clear out all the existing files out of the branch so a Harp app can go there instead.

  ```sh
# Always ensure you’re in the right place before deleting files with this command
  git rm -rf .
  ```
 
3. ### Initialize a Harp app

  Your repository is ready, you just need a Harp app there. Initialize a new Harp app into `_harp`.

  ```sh
  harp init _harp
  ```

  If you have an existing project, you may also move it into your working directory, but make sure to name the folder with an underscore at the beginning; when you deploy to GitHub Pages, you don’t want your source files to be served.

4. ### Compile your Harp app

  Harp can compile your app to <abbr>HTML</abbr>, <abbr>CSS</abbr>, and JavaScript whenever you’d like. By default, `harp compile` creates a `www` directory. Because GitHub Pages are served from the root of the repository, however, you’ll want to compile your Harp app there instead.

  ```sh
  harp compile _harp ./
  ```

5. ### Deploy to GitHub Pages

  You’re ready to deploy your app! Add all the files, commit them, and push them to GitHub:

  ```sh
  git add -A
  git commit -a -m "First Harp + Pages commit"
  git push origin gh-pages
  ```

  Your app will be available at `your-github-name.github.io/repository-name` within the next ten minutes.

##### What’s Next?

Your Harp app has been successfully deployed to GitHub Pages. Now, you’d probably like to customize it. Read the [five simple rules](https://harp.sh/docs/development/rules) for templating a Harp application to get started quickly.

If you’d like to use a custom domain with GitHub pages, follow the instructions in the [GitHub Pages documentation](https://help.github.com/articles/setting-up-a-custom-domain-with-pages).
