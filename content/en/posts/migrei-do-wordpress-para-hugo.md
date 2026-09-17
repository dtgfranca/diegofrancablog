---
title: "I Migrated from WordPress to Hugo"
date: 2025-09-24T16:33:47-03:00
draft: false
---

Well, I think you noticed the blog had a layout change. I'll explain why I made this radical change to my blog, but first I'll tell the story from the beginning.

## Why I decided to start a blog

In 2019, I was, let's say, in a plateau: I couldn't finish any project I started.

That's when the idea of starting a blog came to me — something I could finish quickly, so I wouldn't get discouraged during the creation process.

I chose WordPress, bought a theme and hosting. I set it up and within a few hours everything was configured and published. I was very happy, because I'd finally finished a project.

It took me about seven more months to write the first post. I had no idea what to write about. At the time, I was working on a database migration at the company. I was creating a Docker setup to install MySQL and Oracle, which was a huge challenge, especially with Oracle.

After finishing the setup, I wanted to save the step-by-step for future reference. That's when I remembered the blog, I wrote the first post, published it, and was very happy with it. From that moment on, the blog became a place where I recorded everything I learned and didn't want to forget.

## My frustration with WordPress

That was a brief story about why I decided to start a blog. But after a few years, I started not liking my site's layout and performance — especially on mobile, which wasn't great.

In PageSpeed tests, it always got low scores, and that frustrated me. So I tried to optimize: I added plugins to manage cache, plugins to reduce CSS and JS, and even more plugins to improve performance, plus plugins to set up forms, plugins to manage AdSense and Analytics.

In short, I was programming "plugin-oriented." With so many plugins installed in WordPress, the blog started to get really heavy — and the side menu had gotten so big that my screen couldn't show all the options anymore.

I wanted a site that was simple and fast. I looked for a design to improve the layout and make it as simple as possible. I made the changes, but something inside me still said it wasn't right — I wanted something even simpler: a layout without too much fuss, because my goal is just to write about what I'm practicing.

One of the features that wouldn't let me leave WordPress was the ability to schedule posts, put them in draft, preview posts — simple features, but I didn't see an alternative in another platform.

I saw some people talking about static site generators, studied them very superficially, and dismissed the option right away. Because when I read that posts were created in Markdown and that I had to deploy using Git, in my head that was a step backward and I immediately thought: "I have a very robust environment with WordPress that automates everything."

## Diving into static site generators

That's when I started following [Akita's blog](https://akitaonrails.com/2025/09/10/meu-novo-blog-como-eu-fiz/) and in one of his posts he talked about how he had built his new blog with [Hugo](https://gohugo.io/hugo-modules/) and [Hextra](https://themes.gohugo.io/themes/hextra/). I read it and liked what I saw on his blog.

Since I really like Akita, I decided to run some tests with the tool and evaluate. After all, Akita was using it — so it had to be good.

I installed it on my machine, ran some tests, and really liked the simple layout — basically just HTML. I saw that it had everything I needed to manage a personal blog, and most importantly: I wanted to convert my old posts to this new tool without too much work.

I looked and saw that on the official site they teach how to do this migration with several tools. After running all those tests, I was now ready for the migration.

I did the whole migration and it was simpler than I expected — I didn't even spend 5 hours to migrate and deploy to GitHub Pages.

Now that I've shared my experience, I'll show you how I did the migration step by step:

## Starting the migration

Installing Hugo:

I'm doing this installation on my personal machine running Ubuntu 24.04.3 LTS. In this part, I had an issue installing Hugo via snap. I recommend that, if you're using Linux, you grab it from the GitHub releases page:

https://github.com/gohugoio/hugo/releases

Look for the format that suits you best — in my case it was the `.deb`. Download the file and install it.

To confirm everything is fine, open the terminal and type:

```
hugo version
```

### Exporting data from WordPress:

1 - Go to WordPress and, in the **Tools** menu, select **Export**. Choose the **All posts** option. WordPress will generate an `.xml` file containing all your posts.
[Link to the WordPress documentation](https://wordpress.org/documentation/article/tools-export-screen/)

### Converting to Hugo

With that file in hand, we'll now convert it to Hugo's format. To do that, we'll install a CLI tool called wp2hugo.

My decision to use this tool was simply because it's a CLI tool, doesn't require much configuration, and is easy to use.

### First we clone the repository:

```
$ git clone git@github.com:ashishb/wp2hugo.git
```

Enter the directory:

```
$ cd wp2hugo/src/wp2hugo
```

Now build it:

```
$ make build_prod
```

After compiling, inside that `wp2hugo/src/wp2hugo/bin` directory, you'll have a file called `wp2hugo`. Now we can run that file:

```
$ ./bin/wp2hugo --source wordpress-export.xml --download-media
```

- `--source`: Path to your XML file generated by WordPress.
- `--download-media`: This parameter downloads all the images from your posts. If you don't pass it, it won't download the images.

This command will generate a file with all the WordPress posts already in Hugo's format. Go into the generated directory and run the command:

```
hugo server
```

And you'll see your entire site already in Hugo's pattern, ready to be published. In this post I won't show the step-by-step for publishing — I believe that for those who already maintain a site/blog on WordPress, deploying to Netlify or GitHub Pages should be smoother. I'll leave the links for those two here, but on the site there are several other ways to deploy:

Netlify:

https://gohugo.io/host-and-deploy/host-on-netlify/#article

GitHub Pages:

https://gohugo.io/host-and-deploy/host-on-github-pages/

I'll leave a comparison table between Hugo and WordPress so you can evaluate more calmly:

### WordPress vs Hugo: what changes?

| **Criteria**            | **WordPress**                                                              | **Hugo**                                                                |
|-------------------------|----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Performance**         | Depends on database, PHP, and plugins. Can get heavy.                      | Generates static pages — super fast and lightweight.                    |
| **Complexity**          | Many plugins, themes, and settings.                                        | Simple structure, posts in Markdown, focus on content.                  |
| **Maintenance**         | Requires plugin, theme, and security updates.                              | No database or plugins: almost zero maintenance.                        |
| **Flexibility**         | Huge ecosystem (plugins for everything).                                   | Flexible via code and templates, but no "install and use" approach.     |
| **Ease of use**         | Friendly dashboard, good for non-programmers.                              | Requires dealing with CLI and Git, more technical.                      |
| **Deploy**              | Requires a server (PHP/MySQL).                                             | Can be hosted for free on GitHub Pages, Netlify, or Vercel.             |
| **Post scheduling**     | Native, very practical.                                                    | Also supports future dates via front matter configuration.              |
| **Cost**                | Hosting + possible premium themes/plugins.                                 | Free or very cheap hosting.                                             |

Running the PageSpeed test:

Mobile
{{< figure src="/images/2025/9/pagespeedcelular.png" alt="Image description" caption="" >}}
Desktop
{{< figure src="/images/2025/9/pagespeeddesktop.png" alt="Image description" caption="" >}}

For me, the migration was liberating: I now have a lighter, simpler, and faster site. If you also feel WordPress is getting heavy, I recommend giving Hugo a try.

{{< adsense >}}
