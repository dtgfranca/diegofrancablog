---
categories:
  - uncategorized
cover:
  alt: novo-php8-pt
  image: /wp-content/uploads/2020/12/novo-php8-pt.jpg
date: "2020-12-06T14:08:32+00:00"
title: "PHP 8 is released"
aliases:
  - /2020/12/06/php-8-e-lancado/

---
The PHP development team [announced](https://www.php.net/releases/8.0/en.php) the release of PHP 8 on November 26, 2020:

> _PHP 8.0 is a major update of the PHP language._
>
> _It contains many new features and optimizations including named arguments, union types, attributes, constructor property promotion, match expression, nullsafe operator, JIT, and improvements in the type system, error handling, and consistency._
>
>

Here's a list of some of the new PHP features:

- Union Types
- Named Arguments
- Match Expressions
- Attributes
- Constructor Property Promotion
- Nullsafe Operator
- Weak Maps
- Just In Time Compilation
- and much more…

Here are some highlights of the release:

### PHP 8 NAMED ARGUMENTS

```php
// PHP 7
htmlspecialchars($string, ENT_COMPAT | ENT_HTML401, 'UTF-8', false);

// PHP 8
// Specify only required parameters, skipping optional ones.
// Arguments are order-independent and self-documented.
htmlspecialchars($string, double_encode: false);
```

### PHP 8 ATTRIBUTES

Instead of PHPDoc annotations, you can now use a metadata structure with PHP's native syntax.

```php
// PHP 7
class PostsController
{
    /**
     * @Route("/api/posts/{id}", methods={"GET"})
     */
    public function get($id) { /* ... */ }
}

// PHP 8
class PostsController
{
    #[Route("/api/posts/{id}", methods: ["GET"])]
    public function get($id) { /* ... */ }
}
```

### PHP 8 CONSTRUCTOR PROPERTY PROMOTION

Less code to define and initialize properties.

```php
class Point {
  public float $x;
  public float $y;
  public float $z;

  public function __construct(
    float $x = 0.0,
    float $y = 0.0,
    float $z = 0.0,
  ) {
    $this->x = $x;
    $this->y = $y;
    $this->z = $z;
  }
}

// PHP 8
class Point {
  public function __construct(
    public float $x = 0.0,
    public float $y = 0.0,
    public float $z = 0.0,
  ) {}
}
```

### PHP 8 UNION TYPES

Instead of PHPDoc annotations for type combinations, you can use a union type declaration that's validated at runtime.

```php
// PHP 7
class Number {
  /** @var int|float */
  private $number;

  /**
   * @param float|int $number
   */
  public function __construct($number) {
    $this->number = $number;
  }
}

new Number('NaN'); // Ok

// PHP 8
class Number {
  public function __construct(
    private int|float $number
  ) {}
}

new Number('NaN'); // TypeError
```

### PHP 8 Nullsafe Operator

Instead of checking for null in conditions, you can now use a chain of calls with the new nullsafe operator. When the validation of an element fails, the execution of the whole chain is canceled and the entire chain is evaluated as null.

```php
// PHP 7
$country =  null;

if ($session !== null) {
  $user = $session->user;

  if ($user !== null) {
    $address = $user->getAddress();

    if ($address !== null) {
      $country = $address->country;
    }
  }
}

// PHP 8
$country = $session?->user?->getAddress()?->country;
```

### PHP 8 MATCH EXPRESSION

The new `match` is similar to `switch` and has the following features:

- `match` is an expression, meaning it can be stored in a variable or returned.
- A `match` branch only supports a single-line expression and doesn't need a `break;` statement.
- `match` does strict comparisons.

```php
// PHP 7
switch (8.0) {
  case '8.0':
    $result = "Oh no!";
    break;
  case 8.0:
    $result = "This is what I expected";
    break;
}
echo $result;
//> Oh no!

// PHP 8
echo match (8.0) {
  '8.0' => "Oh no!",
  8.0 => "This is what I expected",
};
//> This is what I expected
```

Those were just some highlights of PHP 8. Check out the [official announcement](https://www.php.net/releases/8.0/en.php) for more details.

Source: [Laravel News](https://laravel-news.com/php-8)
