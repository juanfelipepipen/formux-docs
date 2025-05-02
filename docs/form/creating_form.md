---
sidebar_position: 6
---

# Creating a form

Validating forms created with Formux using BLoC is very simple, secure and practical.

To create a form, you must create a class that will contain each input that composes 
it, extending Formux. Below is an example with a login that requires an email and password.

```dart
import 'package:formux/formux.dart';

class LoginForm extends Formux {
  FormuxStringInput email = FormuxStringInput();
  FormuxStringInput password = FormuxStringInput();

  @override
  List<FormuxInput> get inputs => [email, password];
}
```