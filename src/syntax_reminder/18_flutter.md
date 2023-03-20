<!-- markdownlint-disable MD001 -->

# Flutter

- [Stateless widget](#stateless-widget)
- [Stateful widget](#stateful-widget)
- [Dependencies](#dependencies)

### Stateless widget

``` dart
class MyWidget extends StatelessWidget {
  const MyWidget({ Key? key }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      // ...
    );
  }
}
```

### Stateful widget

``` dart
class MyWidget extends StatefulWidget {
  const MyWidget({ Key? key }) : super(key: key);

  @override
  State<MyWidget> createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  @override
  Widget build(BuildContext context) {
    return Container(
      // ...
    );
  }
}
```

### Dependencies

``` yaml
dependencies:
  package_name: ^1.2.3 # < 2.0.0 (caret)
  package_name: ~1.2.3 # < 1.3.0 (tilde)
  package_name: 1.2.* # < 1.3.0 (wildcard)
  package_name: * # > 0.0.0
```
