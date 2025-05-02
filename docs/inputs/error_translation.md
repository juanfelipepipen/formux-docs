---
sidebar_position: 6
---

# Error translation

An input is outside the scope of the BuildContext used in Widgets, so that access can be 
provided without directly relying on any weird handling within the UI.

Each error that is part of an input validation is presented as a text string, so when the 
input generates a validation error, the error is saved in an error list. To add an error 
using our application's localization, there are several ways.

## Default translations

Formux has generic translations available for use; to do this, simply add the Translations 
mixin to your input, and you'll be able to use many commonly used translations that reflect 
validation errors.

```dart
import 'package:formux/formux.dart';

/// Use Translations mixin on input class
class MyInputString extends FormuxInput<String> with Translations {
  ...
  @override
  void validator() {
    /// Use the translations variable to access the available translations
    assertion(value.isEmpty, translations.required);
  }
}
```

For your app to use the user's default localization, you must add the FormuxLocalization delegate 
to your MaterialApp declaration. Otherwise, an exception will be thrown when trying to use 
translations in the input.

```dart
import 'package:formux/formux.dart';

MaterialApp(
  ...
  localizationsDelegates: const [
    /// Add this delegate 
    FormuxLocalization.delegate,
  ],
),
```

## Custom translations

