**This feature is merged into the original [source_gen_test](https://pub.dev/packages/source_gen_test) package as of version 1.1.0. This fork is therefore deprecated.**

This package is similar to [source_gen_test](https://pub.dev/packages/source_gen_test),
but it allows you to compare the output of a generator with a golden Dart file.

## Usage

```dart
part 'goldens/testclass.dart';

@ShouldGenerateFile(
  'goldens/testclass.dart',
  partOfCurrent: true,
  configurations: ['default', 'no-prefix-required'],
)
@TestAnnotation()
class TestClass {}
```

## Rationale

For an example use, see this package: https://github.com/alexeyinkin/dart-enum-map/tree/main/enum_map_gen

The package generates code of 160+ lines.
To verify such a long output, it is useful to not only test that the output matches a string,
but also to write tests on that output itself.

This file uses the `ShouldGenerateFile` annotation:
https://github.com/alexeyinkin/dart-enum-map/blob/main/enum_map_gen/test/unmodifiable_enum_map/src/input.dart

This is the golden that the output is compared with:
https://github.com/alexeyinkin/dart-enum-map/blob/main/enum_map_gen/test/unmodifiable_enum_map/src/output.dart

This is the test on that golden:
https://github.com/alexeyinkin/dart-enum-map/blob/main/enum_map_gen/test/unmodifiable_enum_map/unmodifiable_enum_map_test.dart

This pair of tests ensures that the output both matches the desired one and works as expected.

## Status

This does not have to be a separate package.
There is [a PR to source_gen_test itself](https://github.com/kevmoo/source_gen_test/pull)
that adds this annotation.

Unfortunately, it is not yet merged, but the need for this feature was pushing,
so this separate package was published.
It was copied from `source_gen_test`, then `ShouldGenerate` and `ShouldThrow` were deleted.
So were all the tests that were failing because of the deletion.

This approach is inconvenient, because:

- There is a lot of code duplication.
- Using both packages together is hard.

There was no chance for a more elegant way, because `source_gen_test` is closed for extension.

I expect to deprecate this package when the above PR is merged.

The version of this package matches the version of `source_gen_test` it was synchronized with.
