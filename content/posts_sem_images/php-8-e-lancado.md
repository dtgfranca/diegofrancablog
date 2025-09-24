---
_b2s_post_meta:
  card_desc: |-
    A equipe de desenvolvimento do PHP anunciou o lançamento do PHP 8 no dia, 26 de Novembro de 2020:




    PHP 8.0 is a major update of the PHP language.



    It cont
  card_image: http://diegofranca.dev/wp-content/uploads/2020/12/novo-php8-pt.jpg
  card_title: PHP 8 é lançado
  og_desc: |-
    A equipe de desenvolvimento do PHP anunciou o lançamento do PHP 8 no dia, 26 de Novembro de 2020:




    PHP 8.0 is a major update of the PHP language.



    It cont
  og_image: http://diegofranca.dev/wp-content/uploads/2020/12/novo-php8-pt.jpg
  og_image_alt: ""
  og_title: PHP 8 é lançado
_edit_last: "1"
_thumbnail_id: "318"
author: diego.tg.franca@gmail.com
categories:
  - uncategorized
cover:
  alt: novo-php8-pt
  image: /wp-content/uploads/2020/12/novo-php8-pt.jpg
date: "2020-12-06T14:08:32+00:00"
fw:opt:ext:pb:page-builder:json: '[]'
fw_options:
  page-builder:
    builder_active: false
    json: '[]'
guid: http://diegofranca.dev/?p=315
parent_post_id: null
post_id: "315"
summary: |-
  A equipe de desenvolvimento do PHP [anunciou](https://www.php.net/releases/8.0/en.php) o lançamento do PHP 8 no dia, 26 de Novembro de 2020:

  > _PHP 8.0 is a major update of the PHP language._
  >
  > _It contains many new features and optimizations including named arguments, union types, attributes, constructor property promotion, match expression, nullsafe operator, JIT, and improvements in the type system, error handling, and consistency._
  >
  >
title: PHP 8 é lançado
url: /2020/12/06/php-8-e-lancado/

---
A equipe de desenvolvimento do PHP [anunciou](https://www.php.net/releases/8.0/en.php) o lançamento do PHP 8 no dia, 26 de Novembro de 2020:

> _PHP 8.0 is a major update of the PHP language._
>
> _It contains many new features and optimizations including named arguments, union types, attributes, constructor property promotion, match expression, nullsafe operator, JIT, and improvements in the type system, error handling, and consistency._
>
> 

Aqui está uma lista de algumas novas features do PHP:

- Union Types
- Named Arguments
- Match Expressions
- Attributes
- Constructor Property Promotion
- Nullsafe Operator
- Weak Maps
- Just In Time Compilation
- e muito mais...

Aqui estão alguns dos destaques do lançamento:

### PHP 8 NAMED ARGUMENTS

```
// PHP 7
htmlspecialchars($string, ENT_COMPAT | ENT_HTML401, 'UTF-8', false);

// PHP 8
// Specify only required parameters, skipping optional ones.
// Arguments are order-independent and self-documented.
htmlspecialchars($string, double_encode: false);
```

### PHP 8 ATTRIBUTES

Em vez das anotações do PHPDoc, você pode agora usar estrutura de metadados com a sintaxe nativa do PHP.

```
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

### PHP8 CONSTRUCTOR PROPERTY PROMOTION

Menos código para definir e inicializar propriedades.

```
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

### PHP8 UNION TYPES

Ao invés das annotations do PHPDOC para combinação de tipos, você pode usar declaração union type que são validadas em tempo de execução.

```
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

### PHP8 Nullsafe Operator

Ao invés de chechar o valor null nas condições, você agora pode usar uma cadeia de chamadas com o novo operador nullsafe. Quando a validação de um elemento falhar, a execução de toda a chain é cancelada e toda a chain é avaliada como null.

```
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

### PHP8 MATCH EXPRESSION

O novo match é similar ao switch e tem as seguintes funcionalidades:

- Match é um expressão, significa que pode ser armazenada em uma varíavel ou retorná-la;
- Match branch somente suporta uma expressão single-line e não precisa de um break ; statement;
- Match faz comparações estritas.

```
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

Isso foi apenas alguns dos destaques do PHP8. Confira o [anunciamento oficial](https://www.php.net/releases/8.0/en.php) para mais detalhes.

Fonte: [Laravel News](https://laravel-news.com/php-8)
