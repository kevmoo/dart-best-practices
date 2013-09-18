#Define the type paramater for operator== as Object

Equality checks happen all the time in programming. A great example is `List.contains`.

Don't cause runtime exceptions in `==` by expecting only the same type as a paramater.

## Example
Instead of:

```dart
class Foo {
  final int value;

  bool operator==(Foo other) => other.value == value;
}
```

Do this:

```dart
class Foo {
  final int value;

  bool operator==(Object other) => other is Foo && other.value == value;
}
```

