# Multi-backed enum

<p align="center">
  <a href="https://github.com/try-again-later/MultiBackedEnum/actions/workflows/test.yml">
    <img
      src="https://github.com/try-again-later/multibackedenum/actions/workflows/test.yml/badge.svg"
      alt="Tests"
    >
  </a>
  <a href="https://packagist.org/packages/try-again-later/multi-backed-enum">
    <img
      src="https://img.shields.io/packagist/v/try-again-later/multi-backed-enum"
      alt="Latest Version"
    >
  </a>
  <a href="https://packagist.org/packages/try-again-later/multi-backed-enum">
    <img
      src="https://img.shields.io/packagist/l/try-again-later/multi-backed-enum"
      alt="Latest Version"
    >
  </a>
</p>

Just a proof of concept and me playing around with PHP 8 attributes.

A small PHP library for creating enums with cases backed by multiple values. Useful when you have a
bunch of "backing" values (strings or numbers) all of which identify the same thing.

The interface mimics PHP 8.1.0 backed enums with an addition of method `allValues()`, which returns
a list of all "backing" values.

## Installation

Via composer:

```sh
$ composer require try-again-later/multi-backed-enum
```

## Example

```php
use TryAgainLater\MultiBackedEnum\{MultiBackedEnum, Values, MakeMultiBacked};

#[MultiBackedEnum]
enum Status
{
  #[Values('on', 'true', 'yes')]
  case ON;

  #[Values('off', 'false', 'no', 'null')]
  case OFF;

  use MakeMultiBacked;
}

// Status::ON
$status = Status::tryFrom('true');

// Throws a ValueError
$status = Status::from('some bad value');

// 'off'
$stringStatus = Status::OFF->value();

// ['on', 'true', 'yes']
$stringStatuses = Status::ON->allValues();
```
