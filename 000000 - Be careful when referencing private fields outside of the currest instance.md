#Be careful when referencing private fields outside of the currest instance

You may be tempted to use to reference private, instance fields for classes in your library.

## Example

```dart
// Library A

int sumFoo(Foo a, Foo b) => a._value + b._value;

class Foo {
  int _value;

  int get value => _value;

  bool operator==(other) => other is Foo && other._value == _value;
}
```

Remember: someone may *implement* your class in another package, or you may forget and implement the original type in the same library.

```dart
// Library B
class Bar implements Foo {
  int _data;

  int get value => _data;
}
```

Now the top-level method `sumFoo` and `operator==` in `Foo` will fail with runtime exceptions.

## Suggestion

```dart
// Library A

int sumFoo(Foo a, Foo b) => a._value + b._value;

class Foo {
  int _value;

  int get value => _value;

  // Don't assume private field in 'other'
  // Okay to use private fields from the current instance
  bool operator==(other) => other is Foo && other.value == _value;
}
```
