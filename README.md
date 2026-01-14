# Suave.Minify

A minify and bundling WebPart for [Suave](https://suave.io/) using [YUI Compressor](https://github.com/YUICompressor-NET/YUICompressor.NET).

[![NuGet](https://img.shields.io/nuget/v/Suave.Minify.svg)](https://www.nuget.org/packages/Suave.Minify/)
[![Build status](https://ci.appveyor.com/api/projects/status/ny7hk6bo7gv9s97m?svg=true)](https://ci.appveyor.com/project/AdemarGonzalez/suave-minify)

## Features

- **JavaScript minification** - Compress JavaScript files using YUI Compressor
- **CSS minification** - Compress CSS files using YUI Compressor
- **Bundling** - Combine multiple files into a single response
- **Caching** - Automatic in-memory caching of minified content
- **Conditional requests** - Supports `If-Modified-Since` header for efficient browser caching
- **Pre-minified file support** - Files containing `.min.` in the name are included without re-minification

## Installation

```bash
dotnet add package Suave.Minify
```

## Usage

### JavaScript Bundle

Bundle and minify multiple JavaScript files:

```fsharp
open Suave
open Suave.Filters
open Suave.Minify

let app : WebPart =
    path "/jsbundle" >=> jsBundle [ "js/jquery-3.1.1.min.js"; "js/chess.js"; "js/app.js" ]
```

### CSS Bundle

Bundle and minify multiple CSS files:

```fsharp
open Suave
open Suave.Filters
open Suave.Minify

let app : WebPart =
    path "/styles/bundle.css" >=> cssBundle [ "styles/main.css"; "styles/layout.css" ]
```

### Manual Compression

You can also use the lower-level `compress` function directly:

```fsharp
open Suave.Minify

// Compress a list of JavaScript files
let minifiedJs = compress [ "path/to/file1.js"; "path/to/file2.js" ] "*.js"

// Compress a list of CSS files  
let minifiedCss = compress [ "path/to/file1.css"; "path/to/file2.css" ] "*.css"
```

## API Reference

| Function | Description |
|----------|-------------|
| `jsBundle` | Creates a WebPart that serves bundled and minified JavaScript with `application/x-javascript` MIME type |
| `cssBundle` | Creates a WebPart that serves bundled and minified CSS with `text/css` MIME type |
| `bundle` | Lower-level function to create a bundling WebPart with a custom filter |
| `compress` | Compresses a list of files and returns the minified content as a string |
| `mimify` | Cached version of `compress` - returns cached result if available |

## Notes

- Files with `.min.` in the filename (e.g., `jquery.min.js`) are included as-is without additional minification
- The library caches minified content in memory for performance
- Supports `If-Modified-Since` HTTP header for browser caching

## Requirements

- .NET 10.0 or later
- Suave 3.2.2 or later

## Dependencies

- [YUICompressor.NET](https://github.com/YUICompressor-NET/YUICompressor.NET) - JavaScript and CSS minification
- [EcmaScript.Net](https://www.nuget.org/packages/EcmaScript.Net) - ECMAScript parsing

## License

This project is part of the [Suave](https://github.com/SuaveIO) ecosystem.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

