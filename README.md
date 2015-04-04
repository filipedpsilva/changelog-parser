# changelog-parser

[![](https://img.shields.io/npm/v/changelog-parser.svg?style=flat-square)](https://www.npmjs.com/package/changelog-parser)
[![](https://img.shields.io/travis/ngoldman/changelog-parser.svg?style=flat-square)](https://travis-ci.org/ngoldman/changelog-parser)

Change log parser for node.

## Usage

```
npm install changelog-parser
```

```js
var parseChangelog = require('changelog-parser')

parseChangelog('path/to/CHANGELOG.md', function (err, result) {
  if (err) throw err

  // changelog object
  console.log(result)
})
```

## Command-line interface

There is also a command-line interface available if you install it with `-g`.

```
npm install -g changelog-parser
```

This installs a program called `changelog-parser` that you simply pass a `CHANGELOG.md` file.

```
changelog-parser path/to/CHANGELOG.md
```

This will print the JSON object representing the change log to the terminal.

Alternately you can run it without arguments and it will look for a `CHANGELOG.md` file in the working directory.

## Standards

This module assumes your changelog is:

1. A markdown file
1. Structured roughly like so:

```md
# changelog title

A cool description (optional).

## unreleased
* foo

## x.y.z - YYYY-MM-DD
* bar

## [a.b.c]

### Changes

* Update API
* Fix bug #1

## 2.2.3-pre.1 - 2013-02-14
* Update API

## 2.0.0-x.7.z.92 - 2013-02-14
* bark bark
* woof
* arf

## v1.3.0

* make it so

## [1.2.3](link)
* init

[a.b.c]: http://altavista.com
```

Parsing the above example will return the following object:

```js
{
  title: 'changelog title',
  description: 'A cool description (optional).',
  versions: [
    { version: null,
      title: 'unreleased',
      body: '* foo' },
    { version: 'x.y.z',
      title: 'x.y.z - YYYY-MM-DD',
      body: '* bar' },
    { version: 'a.b.c',
      title: '[a.b.c]',
      body: '### Changes\n\n* Update API\n* Fix bug #1' },
    { version: '2.2.3-pre.1',
      title: '2.2.3-pre.1 - 2013-02-14',
      body: '* Update API' },
    { version: '2.0.0-x.7.z.92',
      title: '2.0.0-x.7.z.92 - 2013-02-14',
      body: '* bark bark\n* woof\n* arf' },
    { version: '1.3.0',
      title: 'v1.3.0',
      body: '* make it so' },
    { version: '1.2.3',
      title: '[1.2.3](link)',
      body: '* init' }
  ]
}
```

Expects versions to be [semver](http://semver.org/) compliant, otherwise sets `version` to null.

`CHANGELOG.md` standards are inspired by [keepachangelog.com](http://keepachangelog.com/).

## Contributing

`changelog-parser` is an **OPEN Open Source Project**. This means that:

> Individuals making significant and valuable contributions are given commit-access to the project to contribute as they see fit. This project is more like an open wiki than a standard guarded open source project.

See the [CONTRIBUTING.md](CONTRIBUTING.md) file for more details.

## License

[ISC](LICENSE.md)
