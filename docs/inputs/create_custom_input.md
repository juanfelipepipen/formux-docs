---
sidebar_position: 6
---

# Create custom input

The idea behind having inputs is that each input has its own capability parameters, such as length,
accepted values, ranges, etc., all of which can be customized and controlled by the user or developer.

En el siguiente ejemplo, podemos ver lo siguiente:

- El input extiende de FormuxInput, en el cual, se debe definir el tipo de dato que tendra el input
- Por defecto, todo input es requerido, pero, esto se puede cambiar al momento de construirlo
- El metodo "validator" es el encargado de hacer las comparaciones para validar si el valor del input es correcto, de lo contrario, se agrega un mensaje de error al input

```dart
class MyInputString extends FormuxInput<String> with Translations {
  MyInputString({
    String? value,
    this.length,
    this.maxLength = 255,
    super.required,
  }) : super(value: value ?? '');

  factory MyInputString.notRequired({String? value, int? length}) =>
      MyInputString(required: false, value: value, length: length);

  int maxLength;
  int? length;

  @override
  void validator() {
    assertion(value.isEmpty, translations.required);
    assertion(value.length > maxLength, translations.fixedLength(maxLength));
  }
}

```