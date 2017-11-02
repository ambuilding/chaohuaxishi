---
layout: post
title: Regular Expressions
---


## PHP's Regular Expressions Support

- [PHP's Regular Expressions Support(github-regex.php)](https://github.com/ambuilding/LevelUp/blob/master/regex.php)

## Character Sets

- `/[w]{3}/` `/[w]{3,5}/` `/[w]*/` `/[w]+/` `/[w]?/` `/www\.([^\.]+)/`

## Greediness

- `/@(\w+)/` `<a href="https://www.dniya.com/$1">$1</a>` `[a-zA-Z0-9_]`

## Lookaheads and Lookbehinds

- `/google(?=<)/i` `/google(?!<)/i` `(?=string) (?!string) (?<=string) (?<!string)`

```
$string = '$name = "Dniya"; My name is Dniya.';

$result = preg_replace('/(?<=\$)name/', 'VARIABLE', $string);

var_dump($result);
```

## Link
- [RegExr is an online tool to learn, build, & test Regular Expressions (RegEx / RegExp):](https://regexr.com/) https://regexr.com/

- [A live regular expression tester for PHP:](http://www.phpliveregex.com) http://www.phpliveregex.com

- https://regexper.com
