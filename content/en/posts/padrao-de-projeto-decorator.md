---
  card_desc: A few days ago, I was working on a system responsible for syncing data between two systems. The new task required reusing that same system to sync
  card_image: http://diegofranca.dev/wp-content/uploads/2025/07/design.png
  card_title: Decorator Design Pattern
  og_desc: A few days ago, I was working on a system responsible for syncing data between two systems. The new task required reusing that same system to sync
  og_image: http://diegofranca.dev/wp-content/uploads/2025/07/design.png
  og_image_alt:
  og_title: Decorator Design Pattern
_edit_last: "1"
_encloseme: "1"
_pingme: "1"
_thumbnail_id: "664"
author: diego.tg.franca@gmail.com
  - design-patterns
  - tips
  - php
  alt: design
  image: /wp-content/uploads/2025/07/design.png
date: "2025-07-08T12:59:17+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
  page-builder: {}
    builder_active: false
    json: '[]'
guid: https://diegofranca.dev/?p=595
parent_post_id: null
pms-content-restrict-custom-non-member-redirect-url:
pms-content-restrict-custom-redirect-url:
pms-content-restrict-message-logged_out:
pms-content-restrict-message-non_members:
pms-content-restrict-type: default
post_id: "595"
  - '#designpatterns'
  - architecture
  - software-engineering
  - php
title: Decorator Design Pattern
  - /2025/07/08/padrao-de-projeto-decorator/
---
A few days ago, I was working on a system responsible for syncing data between two systems. The new task required reusing that same system to sync with a **third** one, but with a few extras: I wanted to send a notification at the start, another at the end, add logs, and accept more parameters.

The problem? That method was already being used in several places in the system. Changing it directly would make the code fragile and pose a high risk of breaking other parts.

That's when I remembered a class on Design Patterns, where the professor explained the **Decorator** pattern. At that moment, everything clicked: I could "decorate" my function with new behaviors — without touching the original code!

## What is the Decorator pattern?

The **Decorator** pattern lets you add extra functionality to an object dynamically — without changing the original class's structure.

Imagine you have a cup of coffee. Sometimes you want plain coffee, sometimes with milk, chocolate, whipped cream… or with all of those together! You don't need to create a class for every possible combination — you just keep "decorating" the base with the add-ons you want.

To illustrate it better, picture this diagram:

{{< figure src="/wp-content/uploads/2025/07/image.png" alt="" caption="" >}}

Still confusing? Hold on, I'll use a simpler example — and I'm sure you'll leave here understanding everything!

## Practical example with coffee

You start with a `CafePuro` (which dev doesn't love a good coffee while programming? :D), and you can add `Leite` (milk), `Acucar` (sugar), `Chantilly` (whipped cream) — and keep combining them however you want.

Let's start with a `CafePuro`. Then, we can add `Leite`, `Acucar`, `Chantilly`... and combine them however we want.

Let's create our component interface, called `Cafe`. It defines the methods that return the **description** and the **price** of the coffee:

```
interface Cafe
{
    public function getDescricao(): string;
    public function getPreco(): float;
}
```

Now we create the `CafePuro` class, which implements the `Cafe` interface:

```
class CafePuro implements Cafe
{
    public function getDescricao(): string
    {
        return "Café puro";
    }

    public function getPreco(): float
    {
        return 0.5;
    }
}
```

Then we create the `CafeDecorator` class, which will be the **base for all of our decorators**:

```
class CafeDecorator implements Cafe
{
    public function __construct(private readonly Cafe $cafe)
    {
    }

    public function getDescricao(): string
    {
        return $this->cafe->getDescricao();
    }

    public function getPreco(): float
    {
        return $this->cafe->getPreco();
    }
}
```

Now our decorators (`Leite`, `Acucar`, `Chantilly`) will extend `CafeDecorator` and override the methods:

**Leite class:**

```
class Leite extends CafeDecorator
{
    public function __construct(private Cafe $decorator)
    {
    }

    #[\Override]
    public function getDescricao(): string
    {
        return $this->decorator->getDescricao() . ' + Leite';
    }

    #[\Override]
    public function getPreco(): float
    {
        return $this->decorator->getPreco() + 1.30;
    }
}
```

**Chantilly class:**

```
class Chantilly extends CafeDecorator
{
    public function __construct(private Cafe $decorator)
    {
    }

    #[\Override]
    public function getDescricao(): string
    {
        return $this->decorator->getDescricao() . ' + Chantilly';
    }

    #[\Override]
    public function getPreco(): float
    {
        return $this->decorator->getPreco() + 1.00;
    }
}
```

**Acucar class:**

```
class Acucar extends CafeDecorator
{
    public function __construct(private Cafe $decorator)
    {
    }

    #[\Override]
    public function getDescricao(): string
    {
        return $this->decorator->getDescricao() . ' + Açucar';
    }

    #[\Override]
    public function getPreco(): float
    {
        return $this->decorator->getPreco() + 2.00;
    }
}
```

With the classes ready, let's look at the **client code** — that is, how we actually use these decorators in practice.

We start with a plain coffee:

To make it more didactic, first we'll "make" a plain coffee:

```
$cafe = new CafePuro();

echo $cafe->getDescricao() . "\n"; // Café Puro
echo $cafe->getPreco() . "\n"; // 0.5
```

Now we want to add milk to the coffee. To do that, just **pass the previous instance** to the `Leite` class's constructor:

```
$cafe = new \Dtgfranca\Decorator\Leite($cafe);
echo $cafe->getDescricao() . "\n"; // Output: Café Puro + Leite
echo $cafe->getPreco() . "\n"; // Output: 1.8
```

Then we add **sugar**:

```
// Adds the sugar
$cafe = new \Dtgfranca\Decorator\Acucar($cafe);

echo $cafe->getDescricao() . "\n"; // Output: Café Puro + Leite + Açucar
echo $cafe->getPreco() . "\n"; // Output: 3.8
```

And finally, the **whipped cream**:

```
// Adds the whipped cream
$cafe = new \Dtgfranca\Decorator\Chantilly($cafe);
echo $cafe->getDescricao() . "\n"; // Output: Café Puro + Leite + Açucar + Chantilly
echo $cafe->getPreco() . "\n"; // Output: 3.8
```

Notice that we managed to **add new behaviors without modifying the original class** (`CafePuro`). That's exactly the spirit of the **Open/Closed Principle** from SOLID:

"Open for extension, closed for modification."

When we want to add something new, we don't change what already exists — we just **extend** it with a decorator.

Another principle applied here is the **Single Responsibility Principle (SRP)**. Each class has only one reason to change. For example: `CafePuro` would only change if the coffee's price or description changed. The extra behavior (milk, sugar, etc.) is isolated in the decorators.

This approach may look simple, but it's **very powerful**. In legacy projects, where touching old code can generate unexpected bugs, using the **Decorator** pattern is an elegant and safe way to add extra behavior.

The full code is available on GitHub, in case you want to test it and play with other combinations:

[https://github.dev/dtgfranca/design-pattern-decorator](https://github.dev/dtgfranca/design-pattern-decorator)

{{< adsense >}}
