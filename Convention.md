# Overview

- [Branch naming](#branch-naming)
- [Code style guide](#code-style-guide)
  - [Dart](#dart)
  - [Kotlin](#kotlin)
  - [Swift](#swift)
- [Versioning and Changelog](#versioning-and-changelog)
- [Markdown style guide](#markdown-style-guide)
- [Git hooks](#git-hooks)
- [Review process](#review-process)
- [Development setup](#development-setup)
- [Project structure](#project-structure)

## Branch naming

The name of a branch consists of: `<Prefix>/<Issue ID>-<Issue Name>`

**Prefix**

The prefix is one of the commit types from [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/), so e.g. a bug fix branch would be named **fix/...**.

Additionaly there's the prefix `investigate` for investigating e.g. plugins, architectures.

**Issue ID**

Just the ID of the issue.

**Issue Name**

Name of the issue in lowercase with whitespaces replaced by hyphens e.g. **add-new-feature**

### Examples

* `fix/1-fix-big-bug`
* `feat/2-add-new-feature`
* `docs/3-add-description-in-readme`
* `investigate/4-investigate-server-connection-plugin`

### Workflow

1. Navigate to the issue for which you want to create a branch.
2. Click the down arrow next to `Create merge request`.
3. Choose if you just want to create a branch or additionally create a MR.
4. GitLab has automatically created `<Issue ID>-<Issue Name>` and you just have to add the `<prefix>/` part.
5. Click `Create merge request` or `Create branch` according to your previous choice.

## Code style guide 
### Dart
We follow the rules of [Effective Dart](https://dart.dev/guides/language/effective-dart) and use the [flutter_lints package](https://pub.dev/packages/flutter_lints) as recommended set of linter rules.
They are enforced by the [Dart Formatter](https://pub.dev/packages/dart_style) and the [Dart Analyzer](https://pub.dev/packages/analyzer).

Formatting can be automatically done on save when the following is included in the workspace settings (`./.vscode/settings.json`):
```json
"editor.formatOnSave": true,
```
[All linter rules](https://dart.dev/tools/linter-rules)

**Additional rules**
<details>
<summary>Click to expand</summary>

### **DO** declare return types.
linter rule: [`always_declare_return_types`](https://dart.dev/tools/linter-rules#always_declare_return_types).

### **AVOID** bool literals in conditional expressions.
linter rule: [`avoid_bool_literals_in_conditional_expressions`](https://dart.dev/tools/linter-rules#avoid_bool_literals_in_conditional_expressions).

### **AVOID** classes with only static members.
linter rule: [`avoid_classes_with_only_static_members`](https://dart.dev/tools/linter-rules#avoid_classes_with_only_static_members).

### **AVOID** returning null for the return types `bool`, `double`, `int` or `num`.
linter rule: [`avoid_returning_null`](https://dart.dev/tools/linter-rules#avoid_returning_null).

### **AVOID** returning null for `Future`.
linter rule: [`avoid_returning_null_for_future`](https://dart.dev/tools/linter-rules#avoid_returning_null_for_future).

### **AVOID** unused constructor parameters.
linter rule: [`avoid_unused_constructor_parameters`](https://dart.dev/tools/linter-rules#avoid_unused_constructor_parameters).

### **AVOID** async functions that return void.
linter rule: [`avoid_void_async`](https://dart.dev/tools/linter-rules#avoid_void_async).

### **DO** use cascade invocations.
linter rule: [`cascade_invocations`](https://dart.dev/tools/linter-rules#cascade_invocations).

### **DON'T** cast a nullable value to a non-nullable value.
linter rule: [`cast_nullable_to_non_nullable`](https://dart.dev/tools/linter-rules#cast_nullable_to_non_nullable).

### **DON'T** invoke asynchronous functions in non-async blocks.
linter rule: [`discarded_futures`](https://dart.dev/tools/linter-rules#discarded_futures).

### **DO** await methods that return a `Future` inside of an async method body.
linter rule: [`unawaited_futures`](https://dart.dev/tools/linter-rules#unawaited_futures).

### **DON'T** test for conditions composed only by literals, since the value can be inferred at compile time.
linter rule: [`literal_only_boolean_expressions`](https://dart.dev/tools/linter-rules#literal_only_boolean_expressions).

### **DO** only throw instances of classes extending either `Exception` or `Error`.
linter rule: [`only_throw_errors`](https://dart.dev/tools/linter-rules#only_throw_errors).

### **DON’T** assign new values to parameters of methods or functions.
linter rule: [`parameter_assignments`](https://dart.dev/tools/linter-rules#parameter_assignments).

### **PREFER** asserts with message.
linter rule: [`prefer_asserts_with_message`](https://dart.dev/tools/linter-rules#prefer_asserts_with_message).

### **DO** use trailing commas for all function calls and declarations.
linter rule: [`require_trailing_commas`](https://dart.dev/tools/linter-rules#require_trailing_commas).

### **DO** use trailing commas on all tree structures longer than one line.
Without trailing commas, code that builds widget trees or similar types of code tends to be hard to read. Adding the trailing commas allows `dart format` to do its job correctly.

Without trailing commas:
```dart
Expanded(
    child: Center(child: Container(width: 64.0, height: 64.0, child: Text("That's a Text"))),
)
```
With trailing commas:
```dart
Expanded(
    child: Center(
        child: Container(
            width: 64.0,
            height: 64.0,
            child: Text("That's a Text"),
        ),
    ),
)
```

### **DO** test type arguments in operator `==(Object other)`.
linter rule: [`test_types_in_equals`](https://dart.dev/tools/linter-rules#test_types_in_equals).

### **AVOID** `throw` in `finally` block.
linter rule: [`throw_in_finally`](https://dart.dev/tools/linter-rules#throw_in_finally).

### **AVOID** unnecessary `await` in return.
linter rule: [`unnecessary_await_in_return`](https://dart.dev/tools/linter-rules#unnecessary_await_in_return).

### **AVOID** unnecessary `final` for local variables.
linter rule: [`unnecessary_final`](https://dart.dev/tools/linter-rules#unnecessary_final).

### **AVOID** unnecessary null aware operator on extension on a nullable type.
linter rule: [`unnecessary_null_aware_operator_on_extension_on_nullable`](https://dart.dev/tools/linter-rules#unnecessary_null_aware_operator_on_extension_on_nullable).

### **AVOID** unnecessary null checks.
linter rule: [`unnecessary_null_checks`](https://dart.dev/tools/linter-rules#unnecessary_null_checks).

### **AVOID** unnecessary paranthesis.
linter rule: [`unnecessary_parenthesis`](https://dart.dev/tools/linter-rules#unnecessary_parenthesis).

### **AVOID** unnecessary raw strings.
linter rule: [`unnecessary_raw_strings`](https://dart.dev/tools/linter-rules#unnecessary_raw_strings).

### **AVOID** unnecessary statements.
linter rule: [`unnecessary_statements`](https://dart.dev/tools/linter-rules#unnecessary_statements).

### **AVOID** unnecessary `toList()` in spreads.
linter rule: [`unnecessary_to_list_in_spreads`](https://dart.dev/tools/linter-rules#unnecessary_to_list_in_spreads).

### **DO** use enums where appropriate.
linter rule: [`use_enums`](https://dart.dev/tools/linter-rules#use_enums).

### **PREFER** the use of `intValue.isOdd/isEven` to check for evenness.
linter rule: [`use_is_even_rather_than_modulo`](https://dart.dev/tools/linter-rules#use_is_even_rather_than_modulo).

### **PREFER** the use of predefined named constants.
linter rule: [`use_named_constants`](https://dart.dev/tools/linter-rules#use_named_constants).

## **DO** use raw string to avoid escapes.
linter rule: [`use_raw_strings`](https://dart.dev/tools/linter-rules#use_raw_strings).

### **DO** use super-initializer parameters where possible.
linter rule: [`use_super_parameters`](https://dart.dev/tools/linter-rules#use_super_parameters).

### **DO** use the `throwsA` matcher instead of try-catch with `fail()`.
linter rule: [`use_test_throws_matchers`](https://dart.dev/tools/linter-rules#use_test_throws_matchers).

### **CONSIDER** exporting publicly visible classes in a single .dart file.
For multiple classes that are used together but are in different files, it’s more convenient for users of your library to import a single file rather many at once. If the user wants narrower imports they can always restrict visibility using the `show` keyword.

This also helps minimize the publicly visible surface.

Example:
```dart
/// In src/apple.dart
class Apple {}

/// In src/orange.dart
class Orange {}

/// In src/veggies.dart
class Potato {}
class Tomato {}

/// In botanical_fruits.dart
export 'src/apple.dart';
export 'src/orange.dart';
// Can also be: export 'src/veggies.dart' hide Potato;
export 'src/veggies.dart' show Tomato;

/// In squeezer.dart
import 'package:plants/botanical_fruits.dart' show Orange;
```

### **DO** use namespacing when there is ambiguity, e.g. in class names.
There are often functions or classes that can collide, e.g. File or Image. If you don't namespace, there will be a compile error.

Good:
```dart
import 'dart:ui' as ui;

import 'package:flutter/material.dart';
...

ui.Image(...) ...
```
Bad:
```dart
import 'dart:ui';

import 'package:flutter/material.dart';
...

Image(...) ... // Which Image is this?
```

### **PREFER** to use show if you only have a few imports from that package. Otherwise, use as.
Using `show` can avoid collisions without requiring you to prepend namespaces to types, leading to cleaner code.

Good:
```dart
import 'package:fancy_style_guide/style.dart' as style;
import 'package:flutter/material.dart';
import 'package:math/simple_functions.dart' show Addition, Subtraction;
```
Bad:
```dart
import 'package:flutter/material.dart' show Container, Row, Column, Padding,
  Expanded, ...;
```

### **PREFER** to use `const` over `final` over `var`.
This minimizes the mutability for each member or local variable.

### **PREFER** return `Widget` instead of a specific type of Flutter widget.
As our project evolves, we may change the widget type that is returned in a function. For example, we might wrap a widget with a Center. Returning Widget simplifies the refactoring, as the method signature wouldn't have to change.

### **PREFER** storing state in Models instead of state.
When storing state that Flutter widgets need to access, prefer to use `ScopedModel` and `ScopedModelDescendant` instead of `StatefulWidget`. A `StatefulWidget` should contain only internal widget state that can be lost without any consequences.

Examples of stuff to store in a `ScopedModel`:
- User selections
- App state
- Anything that needs to be shared by widgets

Examples of stuff to store in a `StatefulWidget`'s State:
- Animation state that doesn't need to be controlled

### **AVOID** mixing named and positional parameters.
Instead, `@required` should be used in place of required positional parameters.

### **PREFER** named parameters.
In most situations, named parameters are less error prone and easier to read than positional parameters, optional or not. They give users to pass in the parameters in whatever order they please, and make Flutter trees especially clearer.

</details>

**Investigation note**
<details>
<summary>Click to expand</summary>

Linter rules we might want to include as well (but I didn't think they were absolutely necessary):
Feel free to check them out.
```yaml
- always_put_control_body_on_new_line
- avoid_annotating_with_dynamic
- avoid_dynamic_calls
- avoid_implementing_value_types
- avoid_type_to_string
- cancel_subscriptions                  # maybe needed for plugin
- close_sinks                           # maybe needed for plugin
- collection_methods_unrelated_type
- deprecated_consistency
- do_not_use_environment
- join_return_with_assignment
- leading_newlines_in_multiline_strings
- no_adjacent_strings_in_list
- prefer_asserts_in_initializer_lists
- prefer_constructors_over_static_methods
- prefer_final_in_for_each
- prefer_foreach
- sized_box_shrink_expand               # only needed for Demo
- use_colored_box                       # only needed for Demo
- use_decorated_box                     # only needed for Demo
```
I excluded rules which are either not yet in a stable Dart SDK or only necessary when compiling to JS.

Linter rules which I didn't find necessary at all:
Additional reasons could be incompatibility with Effective Dart or we don't use a certain feature.
```yaml
- always_put_required_named_parameters_first
- always_specify_types                  # incompatible with Effective Dart style guide
- always_use_package_imports
- avoid_escaping_inner_quotes
- avoid_final_parameters
- prefer_final_parameters
- avoid_multiple_declarations_per_line
- avoid_redundant_argument_values
- avoid_slow_async_io
- conditional_uri_does_not_exist
- diagnostic_describe_all_properties
- eol_at_end_of_file                    # done by .editorconfig
- flutter_style_todos                   # doesn't work with GitLab
- missing_whitespace_between_adjacent_strings
- no_default_cases
- no_runtimeType_toString
- noop_primitive_operations
- prefer_double_quotes
- prefer_single_quotes
- prefer_if_elements_to_conditional_expressions
- prefer_int_literals
- prefer_null_aware_method_calls
- secure_pubspec_urls
- sort_constructors_first
- sort_unnamed_constructors_first
- sort_pub_dependencies
- tighten_type_of_initializing_formals
- prefer_final_locals                   # incompatible with unnecessary_final
- unsafe_html                           # we won't use HTML APIs
- use_late_for_private_fields_and_variables
- use_string_buffers
```
</details>

### Kotlin

We follow the rules of the [Kotlin coding conventions](https://kotlinlang.org/docs/coding-conventions.html) and the [Android Kotlin style guide](https://developer.android.com/kotlin/style-guide). Both are enforced by [ktlint](https://pinterest.github.io/ktlint/) which is in some aspects more strict[\*](https://github.com/pinterest/ktlint/issues/284#issuecomment-425177186). The linter respects the `.editorconfig` file and can be customized if needed.

### Swift

We follow the rules of the [Official raywenderlich.com Swift style guide](https://github.com/kodecocodes/swift-style-guide) which is enforced by [SwiftLint](https://github.com/realm/SwiftLint). The linter can be added to XCode as Build Tool Plugin and there are plugins for [AppCode](https://plugins.jetbrains.com/plugin/9175-swiftlint/) and [VSCode](https://marketplace.visualstudio.com/items?itemName=vknabel.vscode-swiftlint).

## Versioning and Changelog

Our projects `Smart Sensing Library` and `Sensing Plugin` adhere to [Semantic Versioning (SemVer)](https://semver.org/spec/v2.0.0.html). The style guide we use for our changelog is [Common Changelog](https://common-changelog.org/).

Example CHANGELOG.md:

```markdown
# Changelog

## [0.2.1] - 2022-12-24

### Fixed

- Fixed big bug ([#16](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library/-/issues/42)) (Angela Merkel)

## [0.2.0] - 2022-12-12

### Changed

- Changed functionality ([#69](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library/-/issues/69)) (Johnny Sins)

### Added

- Added new feature ([#42](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library/-/issues/42)) (Zaphod Beeblebrox)

## [0.1.0] - 2022-11-16

_Initial release._

[0.2.1]: <https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library/-/releases/0_2_1>
[0.2.0]: <https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library/-/releases/0_2_0>
[0.1.0]: <https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library/-/releases/0_1_0>
```

### Release workflow

1. Create new issue and MR to release new version
2. Update `CHANGELOG.md`
3. Update the version in `pubspec.yaml`
4. Commit, push and merge changes
5. Create release tag to corresponding commit
6. Create release in [GitLab Releases](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library/-/releases) from release tag
7. optional: Update git submodules

## Markdown style guide

GitLab provides some informations how they test there documentation: [GitLab documentation testing](https://docs.gitlab.com/ee/development/documentation/testing.html).

Linters which we can use are [markdownlint](https://github.com/DavidAnson/markdownlint) and [Vale](https://vale.sh/).

markdownlint has an [extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint). Vale has [one](https://marketplace.visualstudio.com/items?itemName=errata-ai.vale-server) as well.

[This](https://gitlab.com/gitlab-org/gitlab/-/blob/master/scripts/lint-doc.sh) could be an example for documentation linting to improve our documentation.

## Git hooks

We can add pre-commit and pre-push hooks to reduce the feedback loop using [lefthook](https://github.com/evilmartians/lefthook).

Once configured it can e.g. check in pre-commit that the formatting and linting is correct and in pre-push run unit tests.

## Review process

1. Checkout branch locally
2. Test added feature/fixed bug
3. Check if changes comply to style guides
4. If you want to comment on something, don't click "Add Comment now" in the MR, but "Start a review" (otherwise the assignee receives an email for each comment)
5. If your review is finished click "Finish review" and eventually add a final comment e.g. "LGTM", "minor improvements required", ...
6. Add code independent comments as thread, so that the assignee has to answer your comment
7. **DON'T** close the threads as assignee, only the reviewers resolve their own threads.
8. **DO** answer an every comment, so that the reviewer sees that you saw the comment. This can be as simple as e.g. "Fixed it", "Added it", "Thanks for the advice".

## Development setup

We use different editors/IDEs for each platform/language:

* Flutter/Dart: [Visual Studio Code](https://code.visualstudio.com/)
* Android/Kotlin: [Android Studio](https://developer.android.com/studio/)
* iOS/Swift: [XCode](https://developer.apple.com/xcode/)

Android Studio and XCode are only required when working on the [Sensing Plugin](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin).

### Editor/IDE setup

**Visual Studio Code**

Install recommended plugins listed in `.\.vscode\extensions.json`:

1. Go to Extensions Tab
2. Enter `@recommended` into the search bar
3. Install every plugin listed under `Workspace Recommendations`

 **Android Studio (Sensing Plugin)**

**DON'T** open `.\android\` or `.\example\` as workspace directory.

1. **DO** open `.\example\android\` so that dependencies are recognized.
1. In the project view (with `Android` selected) three modules are shown: `app`, `sensing_plugin` and `Gradle Scripts`.
1. `app` contains the code for the example and `sensing_plugin` the code for the plugin.
1. Enable EditorConfig support by navigating to `Settings` -> `Editor` -> `Code Style` and check `Enable EditorConfig support`

**XCode (Sensing Plugin)**

**DON'T** open Xcode via right-clicking on the `.\example\ios\` folder and click "Open in Xcode".

1. **DO** open Xcode directly.
1. Click "Open..." or "Cmd + O".
1. Open the `.\example\ios\Runner.xcworkspace`.
1. All things should be initialized automatically.

### Repository setup

We use scripts to execute shell commands for the project setup or to generate code:

* On Linux/MacOS run: `bash <file name>`
* On Windows run: `.\<file name>` Note: They are powershell scripts but work as bash script as well.

For the setup on the [Sensing Plugin](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/sensing-plugin) and [Smart Sensing Library](https://gitlab.uni-ulm.de/se-anwendungsprojekt-22-23/smart-sensing-library) run the `setup.ps1` script.

**Sensing Plugin**

We use the [Pigeon package](https://pub.dev/packages/pigeon) to generate API code for each platform. If you edit \[Insert pigeon file here e.g. `.\pigeons\messages.dart`\] run the `pigeon.ps1` script.

**Smart Sensing Library**

We use the [ObjectBox package](https://pub.dev/packages/objectbox) as database system. If you edit \[Inset object box file here\] run the `objectbox.ps1` script.

## Project structure

Dart provides a [guide](https://dart.dev/guides/libraries/create-library-packages) on how to design a good project structure which we should follow. The following graph should be a basic design of how this would apply on our projects.

```mermaid
graph TD
    A[Root] --> B[lib]
    B --> C[src]
    B --> BA(sensing_plugin.dart)
    C --> CA(sensor_manager.dart)
    C --> CB[generated]
    CB --> CBA(api.dart)
    A --> D[test]
    D --> DA(sensor_manager_test.dart)
    A --> E[tool]
    E --> EA(setup.ps1)
    E --> EB(run_pigeon.ps1)
    A --> F[pigeons]
    F --> FA(api.dart)
```
