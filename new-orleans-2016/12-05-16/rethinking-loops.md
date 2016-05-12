# Rethinking Loops

Sandbox - `composer create-project johnkary/rethinking-loops`

## FizzBuzz

* Coding exercise
* Print 'Fizz' for multiples of 3
* Print 'Buzz' for multiples of 5
* Print 'FizzBuzz' for multiples of both
* Otherwise print the number

## What if We Used Arrays for Everything?

* Collection oriented programming
* Functional programming

## Functional Programming Concepts

* Map - 1:1 transform on a collection
  * `array_map(callable $callback, array $array1 [, array $... ])`
* Filter - Only keep items whre a condition returns true
  * `array_filter(array $array [, callable $callback [, int $flag = 0 ]])`
* Reduce - Combine items into something new
  * `array_reduce(array $array, callable $callback [, mixed $initial = NULL ])`

## Closure

```
function ($param) use ($var) = {
}
```

## Control Structure Anxiety

* Nested control structures :(
* Reduced readibility
* Example:

```
foreach {
  if () {
    foreach () {
      if () {

      }
    }
  }
  else {
    foreach () {
      if () {

      }
    }
  }
}
```

## Notes

Haystack\HArray - Library for pipelining map, filter and reduce functions (https://github.com/ericpoe/haystack)

```
new Haystack\HArray($array)
  ->map(...)
  ->filter(...)
  ->reduce(...)
  ->toArray()
```
