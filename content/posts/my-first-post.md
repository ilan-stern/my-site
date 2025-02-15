+++
date = '2025-02-14T18:19:31+11:00'
draft = false
title = 'Building this site'
+++
I decided to make a blog to track my progress and interests in **Cybersecurity**. 

For this, I'm using ‘Hugo’ -  a static site generator that makes it easy to build fast, simple websites.

---

## Setting up the Site

### 1. Installing Hugo

I started with installing Hugo via the CLI using the command: 

> *brew install hugo*

### 2. Creating a New Hugo test Site

To quickly spin up a test site, I ran the following commands:

> *hugo new site quickstart*

> *cd quickstart*

> *git init*

> *git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke*

> *echo “theme = ‘ananke’” >> hugo.toml*

> *hugo server*

After running hugo server, the terminal provided a local URL where I could view my site in the browser.

---

## Creating My First Post

Once the basic site was running, I created my first post:

> *hugo new content content/posts/my-first-post.md*

After adding this text to the file, I ran: 

> *hugo server -D*

The -D flag ensures that **draft posts** are included in the local preview.

I was able to see my first post! (On the live development server)

---

## Configuring the Site

In the *hugo.toml* file, I configured the baseURL, language code, and title for the site.

---

## Deploying to GitHub Pages

Thanks to the excellent documentation on the gohugo site, this process was a breeze.

### 1. Creating a GitHub Repository

I first created a new repo on GitHub

### 2. Pushing the Local Hugo Site to GitHub

Once the repo was created, I linked my local project to GitHub and pushed the files:

> *git remote add origin <Link to the GitHub Repo>*

> *git branch -M main*

> *git push -u origin main*

### 3. Configuring GitHub Pages

In **GitHub -> Settings -> Pages**, I set the **Source** to "GitHub Actions". 

### 4. Creating the Deployment Workflow

I created the .github/workflows directory and a deployment workflow file:

> *mkdir -p .github/workflows*

> *cd .github/workflows*

> *touch hugo.yaml*

Then, I copied the GitHub Actions deployment script from the Hugo documentation. This scripts defines the steps GitHub Actions follows to build and deploy the site.

---

## Finalising the Deployment

With everything set up, I committed and pushed the new workflow file:

> *git add -A*

> *git commit -m "Created GitHub Actions workflow for deployment"*

> *git push*

Once the workflow ran successfully, I navigated to the **Actions tab** in GitHub to monitor the deployment. After it completed, my blog was live!

---

## Reflections

Overall, this project was a fun and straightforward experience, thanks to Hugo's extensive documentation. I'm excited to continue updating this blog as I progress in my Cybersecurity journey.

This is my first post, and I look forward to sharing more soon!

---

## Resources Used

Hugo Quickstart Guide: https://gohugo.io/getting-started/quick-start/

Hugo Hosting on GitHub Pages: https://gohugo.io/hosting-and-deployment/hosting-on-github/



