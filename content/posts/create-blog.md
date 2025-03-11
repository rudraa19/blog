---
date: 2023-03-11T23:30:26+05:30
title: "Make Your Blog Website Using Hugo"
weight: 1
summary: "Create your blog website in simple steps with the help of Hugo."
---

## Context

This blog post is an extended, detailed version of my YouTube short video:
{{< youtube 0oV-qkZyYIo >}}

## Why Create a Blog Website?

Creating a blog website allows you to share your thoughts, experiences, and knowledge with a wider audience. Whether you're a developer, writer, or hobbyist, a personal blog provides a space to express yourself, build an online presence, and even showcase your work.

## Setting Up Hugo

### Install Hugo

To get started, install Hugo from [gohugo.io](https://gohugo.io/). Follow the installation guide based on your operating system:

- **Windows**: Use Chocolatey or Scoop
- **MacOS**: Use Homebrew (`brew install hugo`)
- **Linux**: Use the package manager (`sudo apt install hugo`)

### Create a New Hugo Site

Once installed, open your terminal and run the following command to create a new Hugo project:

```sh
hugo new site my-blog
```

Replace `my-blog` with your preferred project name.

## Adding a Theme

Hugo provides a variety of themes that can be found at [themes.gohugo.io](https://themes.gohugo.io/). Choose a theme and follow its installation instructions. Generally, you clone the theme into your project’s `themes` directory:

```sh
git clone https://github.com/theme-author/theme-name.git themes/theme-name
```

Then, set the theme in `config.yml`:

```yml
theme: theme-name
```

## Creating Your First Blog Post

Navigate to your Hugo project folder and create a new post:

```sh
hugo new content/post/my-first-blog.md
```

Open the Markdown file and add content. Ensure you include the necessary front matter (headers) as required by your theme:

```md
---
title: "My First Blog Post"
date: 2025-02-08T10:00:00+05:30
draft: false
---

This is my first blog post using Hugo!
```

## Running the Local Server

To preview your website locally, run:

```sh
hugo server
```

Visit `http://localhost:1313/` in your browser to see your blog in action.

## Deploying to Vercel

### Add `vercel.json` File

To deploy your blog on Vercel, create a `vercel.json` file in your project root directory:

```json
{
  "build": {
    "env": {
      "HUGO_VERSION": "0.143.1"
    }
  },
  "buildCommand": "hugo --gc --minify"
}
```

### Deployment Steps

1. Install Vercel CLI (`npm install -g vercel`).
2. Run `vercel` in your project directory and follow the setup prompts.
3. Once deployed, Vercel provides a live URL for your blog.

## Summary

By following these steps, you have successfully created and deployed your blog using Hugo. Now you can focus on writing content and sharing your ideas with the world!

Thank you :)
