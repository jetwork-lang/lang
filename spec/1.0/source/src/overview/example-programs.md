# Example programs

## Simple functions

```
public function isEven(argument: BigInt): Boolean (
    argument % 2 == 0
);

trace(isEven(11));

// https://en.wikipedia.org/wiki/Heron%27s_formula
public function triangleArea(a: Number, b: Number, c: Number): Number {
    const s = (a + b + c) / 2;
    return (s * (s - a) * (s - b) * (s - c)) ** 0.5;
}

trace(triangleArea(5, 6, 7));
```