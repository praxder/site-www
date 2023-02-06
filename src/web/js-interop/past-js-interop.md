---
title: Non-static JS interop
description: Archive of previous JS interop offerings
---

This page addresses previous iterations of JS interop for Dart:
* `dart:js_util`
* `package:js`
* `dart:js`

**We do not recommend using any JS interop solution other than [static interop][].**

Each of these tools still exist and are usable. However, the static interop model
is more performant, provides more capabilities,
and will continue to be supported and developed.
If you are just starting out with JS interop in Dart,
please start with the static interop library, [`js_interop`][].
If you have existing JS interop code implementing one of these tools,
please [refactor your code][] to use the static interop model.

[static interop]: /web/js-interop
[`js_interop`]: {{site.dart-api}}/js_interop
[refactor your code]: /web/js-interop/migration

## `dart:js_util`

[**`dart:js_util` API docs**][]

**We will continue to support `dart:js_util` alongside static interop.**

The `dart:js_util` library, or just `js_util`, is a low-level utility library
for performing JS interop. Because `js_util` is so low-level,
it could potentially be able to provide more flexibility than static interop,
for example, in rare edge cases where `js_interop` is not expressive enough.
This is an exception to the rule;
**please always use static, inline-class based interop by default**.

The `js_util` library is supported by the JS and `dart2wasm` backends.
It is slower and less ergonomic than `js_interop`.

The best example of the difference in ergonomics between `js_interop` and
`js_util` is calling equivalent [`external`][] methods. 
Each interop solution generates JavaScript code upon calling an `external` method:

```dart
// js_util external call:
...

// javascript generated:
...
```

The JavaScript code `external` generates for `js_util` is very verbose,
compared to the efficient, compact generation for `js_interop`:

```dart
// js_interop external call:
...

// javascript generated:
...
```

For optimal JS interop, only use `js_util` over static interop if you encounter
a use case that `js_interop` cannot address
(and please [let us know][] if you encounter such a use case).

[**`dart:js_util` API docs**]: {{site.dart-api}}/dart-js_util/dart-js_util-library.html
[`external`]: /web/js-interop/reference#external
[let us know]: https://github.com/dart-lang/sdk/issues/new?assignees=&labels=web-js-interop&template=1_issue_template.md&title=Create+an+issue

## `package:js`

// *This section probably doesn't make any sense*

[**`package:js` API docs**]

**We will not continue to support `package:js` alongside static interop.**

The `package:js` library can represent objects in different ways with its
class type annotations: 

* [`@JS`] 
* [`@anonymous`]
* [`@staticInterop`]

Because `package:js` supports dynamic invocations of external members (the
opposite of static interop), its static type checking capabilities are
much more limited than static interop, and therefore cannot be fully sound.
For the same reason, `package:js` can not interop with [DOM APIs][]. 

[**`package:js` API docs**]: {{site.pub-pkg}}/js
[`@JS`]: /web/js-interop/reference#js
[`@Anonymous`]: /web/js-interop/reference#others
[`@staticInterop`]: /web/js-interop/reference#staticinterop
[DOM APIs]: /web/js-interop/dom

## `dart:js` 

[**`dart:js` API docs**]

**We will not continue to support `dart:js` alongside static interop.**

The `dart:js` library is a low-level API for non-static interop with JavaScript.
It's wrapper-based model requires much more overhead,
and is much more expensive and slow,
than static interop's zero-cost wrapper model.

[**`dart:js` API docs**]: {{site.dart-api}}/dart-js/dart-js-library.html