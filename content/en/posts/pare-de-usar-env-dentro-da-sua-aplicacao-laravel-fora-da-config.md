---
categories:
  - frameworks
  - php
cover:
  alt: laravel
  image: /wp-content/uploads/2025/06/laravel.png
date: "2025-06-18T18:13:36+00:00"
tags:
  - laravel
  - php
title: "Stop using env() inside your Laravel application (outside of config/)"
aliases:
  - /2025/06/18/pare-de-usar-env-dentro-da-sua-aplicacao-laravel-fora-da-config/

---
I want to share a quick tip about Laravel. I see many people running into trouble when trying to access environment variables inside the application. The most common mistake happens when developers use the `env()` function directly inside their classes or services to read settings from the `.env` file, and then can't figure out why, in some situations, that function returns `null`.

The explanation is simple: it happens because of Laravel's initialization flow. To help visualize it, I created a diagram that explains how this process works:

{{< gallery cols="1" >}}
{{< figure src="/wp-content/uploads/2025/06/ChatGPT-Image-18-de-jun.-de-2025-14_31_46.png" alt="" caption="" >}}
{{< /gallery >}}

As you can see in the image above, when Laravel receives a request (or runs a command, a job, etc.), it starts from the `index.php` file, which calls `bootstrap/app.php`. At that point, Laravel loads the variables from the `.env` file and, right after that, reads the configuration files in the `config/` directory. These settings are then stored in cache (if you run the `php artisan config:cache` command).

After that point, the Service Providers are registered and the application's Kernel takes over the execution. That's why **it's not recommended to use `env()` to access settings after this stage**, because Laravel will no longer depend directly on `.env` during the application's lifecycle.

**Wrong (not recommended outside of `config/`):**

```
env('CHAVE')
```

**Right:**

```
config('configuracao.chave')

```

Following this pattern, you avoid problems with `null` and ensure that your application is compatible with the configuration cache.

{{< adsense >}}
