---
categories:
  - angular
  - tips
  - git
  - javascript
cover:
  alt: demo-4-compressed
  image: /wp-content/uploads/2020/08/demo-4-compressed.png
date: "2020-08-11T14:36:05+00:00"
tags:
  - angular
  - conventional-commits
  - git
title: "GIT - Conventional Commits"
aliases:
  - /2020/08/11/git-conventional-commits/

---
Hey folks, how's it going? Today I'm sharing a tip on how to standardize commit messages in our projects. Sometimes when there's more than one developer on the project and the rush of day-to-day life, the messages end up not being that great. It's very common to see the famous "AD" (various changes) or "VA" (multiple changes), which makes our dev life — which is already not easy — much harder :D.

Conventional Commits was inspired by the [Angular Commit Guidelines](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines) and provides us with a set of rules for creating a commit history, making it easier to write with automated tools. This convention pairs nicely with [SemVer](https://semver.org/), describing features, fixes, and breaking changes.

The commit message should be structured as follows:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

The commit contains the structural elements to communicate the intent to whoever consumes your library:

1. **Fix**: a commit of type `fix` patches a bug in your codebase (this correlates with PATCH in semantic versioning).
2. **Feat**: a commit of type `feat` introduces a new feature to the codebase (this correlates with MINOR in semantic versioning).
3. **BREAKING CHANGE**: a commit that has the footer `BREAKING CHANGE`, or appends `!` after the type/scope, introduces a breaking API change (correlated with MAJOR in semantic versioning). A BREAKING CHANGE can be part of commits of any type.
4. Types other than `fix` and `feat` are allowed — for example, [@commitlint/config-conventional](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional) recommends `build:`, `chore:`, `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, and others.

**INSTALLING GIT COMMIT MSG LINTER**

Luckily for us, some developers created a package that helps us maintain the commit pattern automatically.

For our test I'll use the [git-commit-msg-linter package](https://www.npmjs.com/package/git-commit-msg-linter).

I'll create a simple project to test the plugin. Create a directory called `commit-conventional`:

```
mkdir commit-conventional
```

After running the command above, enter the directory:

```
cd commit-conventional
```

We need to initialize git:

```
git init
```

Now let's create the `package.json` file — for that, run the command (you need to have Node.js installed on your machine):

```
npm init -y
```

Now that we have our `package.json` created, let's install the package:

```
npm install git-commit-msg-linter --save-dev
```

Create any text file:

```
touch test.php
```

Let's add the changes to our staging area:

```
git add .
```

If you still have trouble with git commands, [click here](/2020/08/05/comandos-basicos-do-git/) where I explain some basic commands.

To run the test, execute:

```
git commit -m 'ADD a new file in project'
```

The error shown below will be generated, indicating that our commit doesn't follow the standard.

{{< gallery cols="1" >}}
{{< figure src="/wp-content/uploads/2020/08/Captura-de-Tela-2020-08-11-às-11.13.03.png" alt="" caption="" >}}
{{< /gallery >}}

Now let's commit again, this time following the conventional commits standard:

```
git commit -m "feat: add new file into project"
```

{{< figure src="/wp-content/uploads/2020/08/Captura-de-Tela-2020-08-11-às-11.14.04.png" alt="" caption="" >}}

Now everything is perfect with our commit. You can see how much clearer and more organized our commit messages are.

{{< figure src="/wp-content/uploads/2020/08/Captura-de-Tela-2020-08-11-às-11.14.42.png" alt="" caption="" >}}

I hope you enjoyed this tip. If you have any questions, suggestions, or critiques, leave them in the comments.

**SOURCES:**

[https://www.conventionalcommits.org/en/v1.0.0/](https://www.conventionalcommits.org/en/v1.0.0/)

[https://www.npmjs.com/package/git-commit-msg-linter](https://www.npmjs.com/package/git-commit-msg-linter)

{{< adsense >}}
