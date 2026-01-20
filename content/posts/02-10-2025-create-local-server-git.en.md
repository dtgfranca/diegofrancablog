---
title: "Create a local git server"
date: 2025-11-04T19:19:04-03:00
draft: false
tags:
  - git
  - local-server
  - self-hosted
  - offline-development
  - developer-tools
  - tips
lang: en
translationKey: "local-git-server"
---


Hello everyone!

Today I’d like to share a quick and useful tip: how to create a local Git server. Imagine this situation: you and your colleague are working on an important feature in the office and you need to deliver it in just a few days. Suddenly, the internet goes down — and your mobile data isn’t working either. You urgently need to send the part you just developed to your colleague. Feeling that cold panic already?

Well, did you know it’s possible to have a **local Git server** where you can clone and push without internet, just using your internal network? That’s exactly what I want to show you today. Let’s go!

## Creating a bare repository

First, we need to set up a repository as **bare**. This means it will contain only the Git metadata needed to manage the project versioning. Think of it as a **central hub** that multiple developers can share.

Run the following command to create the bare repository:

```bash
git clone --bare /path-to-your-project /path-to-server/project.git
```

Now that the bare repository has been created, we need to update the server information so we can clone and push from our local server. Use this command:

```bash
git --bare update-server-info && mv hooks/post-update.sample hooks/post-update
```

### Explaining the commands

- `git --bare update-server-info`: Updates the server information in the bare repository and ensures it is configured correctly as a Git server.
- `mv hooks/post-update.sample hooks/post-update`: Enables the *post-update* hook by renaming the sample file.

## Testing your server

To verify everything is working, try cloning the repository using the local path:

```bash
git clone /path-to-server/project.git
```

And that’s it! You now have a **local Git server** ready to use, even without an internet connection.
{{< adsense >}}