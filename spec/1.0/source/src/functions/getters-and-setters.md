# Getters and setters

A function that belongs to a virtual property is either a getter or setter.

```
function get x(): T (v);
function set x(v: T): void {}
```

* Getters and setters must not be asynchronous.
* Getters and setters must not be generators.