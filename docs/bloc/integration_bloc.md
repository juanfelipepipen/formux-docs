---
sidebar_position: 6
---

# Integration with BLoC

Validating forms created with Formux using BLoC is very simple, secure and practical.

In order to use a form in a Cubit, it is essential that the form implements FormuxCopy, 
since, in this way, the Cubit can manipulate the form to control parts of the validation state.

## Form class
For a form to be compatible with CubitForm, it must implement FormuxCopy with the 
definition of the form itself, otherwise, the cubit will not be able to use the form.

```dart
import 'package:formux/formux.dart';

class LoginForm extends Formux<LoginForm> implements FormuxCopy<LoginForm> {
  FormuxEmailInput email = FormuxEmailInput();
  FormuxStringInput password = FormuxStringInput();

  @override
  get inputs => [email, password];

  /// This method allows you to create a copy of the form, you must 
  /// copy the parameters that are essential
  @override
  LoginForm copy() => LoginForm()
    ..email = email
    ..password = password;
}
```

## Cubit class
The cubit mainly only contains the setter methods to set values in
the form, in this example, the user's email and password are received, 
which emit a new state of the form with the new value set.

```dart
import 'package:formux/formux.dart';
import 'login_form.dart';

class LoginCubit extends CubitForm<LoginForm> {
  LoginCubit() : super(LoginForm());

  /// [Setter] Email
  void setEmail(String value) {
    emit(state.copy()..email.value = value);
  }

  /// [Setter] Password
  void setPassword(String value) {
    emit(state.copy()..password.value = value);
  }
}
```