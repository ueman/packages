# cross_file

An abstraction to allow working with files across multiple platforms.

## Usage

Import `package:cross_file/cross_file.dart`, instantiate a `XFile`
using a path or byte array and use its methods and properties to
access the file and its metadata.

Example:

```dart
import 'package:cross_file/cross_file.dart';

final file = XFile('assets/hello.txt');

print('File information:');
print('- Path: ${file.path}');
print('- Name: ${file.name}');
print('- MIME type: ${file.mimeType}');

final fileContent = await file.readAsString();
print('Content of the file: ${fileContent}');  // e.g. "Moto G (4)"
```

```dart
import 'package:cross_file/cross_file.dart';
import 'package:flutter/material.dart';

// create file
final file = XFile('assets/hello.txt');

// use XFileImage with XFile to show it as an image
final image = Image(image: XFileImage(file));
```

You will find links to the API docs on the [pub page](https://pub.dev/packages/cross_file).

## Web Limitations

`XFile` on the web platform is backed by [Blob](https://api.dart.dev/be/180361/dart-html/Blob-class.html)
objects and their URLs.

It seems that Safari hangs when reading Blobs larger than 4GB (your app will stop
without returning any data, or throwing an exception).

This package will attempt to throw an `Exception` before a large file is accessed
from Safari (if its size is known beforehand), so that case can be handled
programmatically.

### Browser compatibility

[![Data on Global support for Blob constructing](https://caniuse.bitsofco.de/image/blobbuilder.png)](https://caniuse.com/blobbuilder)

[![Data on Global support for Blob URLs](https://caniuse.bitsofco.de/image/bloburls.png)](https://caniuse.com/bloburls)
