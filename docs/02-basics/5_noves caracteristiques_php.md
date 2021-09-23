---
layout: default
title: 5. Noves característiques de PHP 7
parent: 2. Característiques bàsiques del llenguatge
nav_order: 5
has_children: false
---

# Noves caracterísques PHP 7

## Spaceship operator  (<==>)
Compara dues expressions $a i $b i torna -1 si $a és menor que $b, 0 si són iguals i 1 si $b és major que $a.

Exemple:

```php
// Integers
echo 1 <=> 1; // 0
echo 1 <=> 2; // -1
echo 2 <=> 1; // 1
```
## Operador de fusió de null ?? 

Torna el primer operand si existeix i no és NULL o el segon operand.

Exemple:

```php
// Fetches the value of $_GET['user'] and returns 'nobody'
// if it does not exist.
$username = $_GET['user'] ?? 'nobody';

// This is equivalent to:
$username = isset($_GET['user']) ? $_GET['user'] : 'nobody';
```

## Més recursos:

* [Noves característiques PHP 7.0](https://www.php.net/manual/es/migration70.new-features.php)
* [Noves característiques PHP 7.1](https://www.php.net/manual/es/migration71.new-features.php)
* [Noves característiques PHP 7.2](https://www.php.net/manual/es/migration72.new-features.php)
* [Noves característiques PHP 7.3](https://www.php.net/manual/es/migration73.new-features.php)
* [Noves característiques PHP 7.4](https://www.php.net/manual/es/migration74.new-features.php)
* [Noves característiques PHP 8.0](https://www.php.net/manual/es/migration80.new-features.php)